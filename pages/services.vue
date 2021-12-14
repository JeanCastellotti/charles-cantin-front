<template>
  <div>
    <h1 class="font-neucha text-5xl text-gray-800 mb-5">Tarifs</h1>
    <div class="grid md:grid-cols-2 gap-4 md:gap-8">
      <BaseCard
        v-for="service in services"
        :key="service.id"
        class="flex flex-col items-center transition transform hover:scale-105 hover:-rotate-1"
      >
        <h2 class="text-gray-500 font-neucha text-3xl mb-5">
          {{ service.title }}
        </h2>
        <p class="mb-5 text-gray-400 font-inter leading-loose text-center">
          {{ service.description }}
        </p>
        <span
          v-if="service.price"
          class="self-stretch text-center pt-5 border-t border-gray-200 font-inter font-thin text-5xl text-gray-600"
        >
          {{ service.price }}€
        </span>
      </BaseCard>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      services: [],
      strapi: 'https://blooming-crag-03388.herokuapp.com/',
    }
  },
  head: {
    title: 'Tarifs et prestations - Charles Cantin',
  },
  async fetch() {
    const services = await fetch(`${this.strapi}/services`).then((r) =>
      r.json()
    )

    this.services = services.map((service) => {
      return {
        id: service.id,
        title: service.title,
        price: service.price,
        description: service.description,
      }
    })
  },
}
</script>
