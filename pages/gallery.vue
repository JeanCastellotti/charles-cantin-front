<template>
  <div>
    <BaseModal v-if="isModalVisible" @close-modal="closeModal" class="h-full">
      <img :src="currentImage" class="max-h-full object-cover rounded" />
    </BaseModal>
    <div class="flex justify-between items-center mb-5">
      <h1 class="font-neucha text-5xl text-gray-800">Galerie</h1>
      <select
        class="rounded bg-white p-4 text-gray-800 font-inter focus:outline-none"
        v-model="currentCategory"
      >
        <option value="all">Toutes les photos</option>
        <option
          v-for="category in categories"
          :value="category.slug"
          :key="category.id"
        >
          {{ category.label }}
        </option>
      </select>
    </div>
    <div
      v-if="!!filteredImages.length"
      class="grid md:grid-cols-2 gap-4 md:gap-8"
    >
      <img
        v-for="image in filteredImages"
        :src="image.url.medium"
        :alt="image.category"
        :key="image.id"
        @click="showModal(image.url.large)"
        class="object-cover h-64 w-full rounded transition transform hover:scale-105 hover:-rotate-1 cursor-pointer"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      categories: [],
      isModalVisible: false,
      currentImage: null,
      currentCategory: 'all',
      strapi: 'https://blooming-crag-03388.herokuapp.com',
    }
  },
  methods: {
    showModal(image) {
      if (window.innerWidth <= 450) return
      this.isModalVisible = true
      this.currentImage = image
    },
    closeModal() {
      this.isModalVisible = false
      this.currentImage = null
    },
  },
  computed: {
    filteredImages() {
      if (this.currentCategory !== 'all')
        return this.images.filter(
          (image) => image.category === this.currentCategory
        )

      return this.images
    },
  },
  head: {
    title: 'Galerie - Charles Cantin',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Découvrez toutes mes réalisations classées par catégorie.',
      },
    ],
  },
  async fetch() {
    const photos = await fetch(`${this.strapi}/photos`).then((r) => r.json())

    this.categories = photos
      .map((photo) => {
        return {
          id: photo.category.id,
          label: photo.category.label,
          slug: photo.category.slug,
        }
      })
      .filter((category, index, arr) => {
        return index === arr.findIndex((cat) => cat.id === category.id)
      })

    this.images = photos.map((photo) => {
      return {
        id: photo.id,
        url: {
          medium: photo.image.formats.medium.url.startsWith('http')
            ? photo.image.formats.medium.url
            : this.strapi + photo.image.formats.medium.url,
          large: photo.image.formats.large.url.startsWith('http')
            ? photo.image.formats.large.url
            : this.strapi + photo.image.formats.large.url,
        },
        category: photo.category.slug,
      }
    })
  },
}
</script>
