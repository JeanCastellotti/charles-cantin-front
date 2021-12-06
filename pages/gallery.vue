<template>
  <div>
    <BaseModal v-if="isModalVisible" @close-modal="closeModal" class="h-full">
      <img
        :src="`${apiUrl}${currentImage}`"
        class="max-h-full object-cover rounded"
      />
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
        :src="`${apiUrl}${image.url.medium}`"
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
      currentCategory: "all",
      apiUrl: "https://dry-ocean-52526.herokuapp.com",
    };
  },
  methods: {
    showModal(image) {
      this.isModalVisible = true;
      this.currentImage = image;
    },
    closeModal() {
      this.isModalVisible = false;
      this.currentImage = null;
    },
  },
  computed: {
    filteredImages() {
      if (this.currentCategory !== "all")
        return this.images.filter(
          (image) => image.category === this.currentCategory
        );

      return this.images;
    },
  },
  head: {
    title: "Galerie - Charles Cantin",
  },
  async fetch() {
    const photos = await fetch(
      `${this.apiUrl}/api/photos?populate=image,category`
    ).then((r) => r.json());

    this.categories = photos.data.map((photo) => {
      return {
        id: photo.attributes.category.id,
        label: photo.attributes.category.data.attributes.label,
        slug: photo.attributes.category.data.attributes.slug,
      };
    });

    this.images = photos.data.map((photo) => {
      return {
        id: photo.id,
        url: {
          medium: photo.attributes.image.data.attributes.formats.medium.url,
          large: photo.attributes.image.data.attributes.formats.large.url,
        },
        category: photo.attributes.category.data.attributes.slug,
      };
    });
  },
};
</script>
