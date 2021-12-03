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
          {{ service.body }}
        </p>
        <span
          v-if="service.price"
          class="self-stretch text-center pt-5 border-t border-gray-200 font-inter font-thin text-5xl text-gray-600"
          >{{ service.price }}€</span
        >
      </BaseCard>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      services: [
        {
          id: 1,
          title: "Juste moi",
          body: "Séance pour une personne, en extérieur ou en studio",
          price: 130,
        },
        {
          id: 2,
          title: "Pour deux",
          body: "Pour deux personnes, en extérieur ou en studio",
          price: 195,
        },
        {
          id: 3,
          title: "Famille",
          body: "Pour la famille ou les amis jusqu’à 4 personnes, en extérieur ou en studio 30 euros en supplément par personne au-delà de 4 (hormis enfant jusqu’à 2 ans)",
          price: 220,
        },
        {
          id: 4,
          title: "Il était une fois",
          body: "Photo de grossesse (À votre domicile, en extérieur ou en studio)",
          price: 160,
        },
        {
          id: 5,
          title: "Mon bébé",
          body: "Photo d’enfant jusqu’à 3 ans (photo à domicile)",
          price: 100,
        },
        {
          id: 6,
          title: "J’immortalise l’événement",
          body: "Prestation de mariage ou baptême sur devis",
          price: null,
        },
      ],
    };
  },
  head: {
    title: "Tarifs et prestations - Charles Cantin",
  },
};
</script>
