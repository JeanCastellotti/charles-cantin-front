<template>
  <div>
    <BaseModal v-if="isModalVisible" @close-modal="closeModal" class="h-full">
      <nuxt-img :src="currentImage" class="max-h-full object-cover rounded" />
    </BaseModal>
    <div class="flex justify-between items-center mb-5">
      <h1 class="font-neucha text-5xl text-gray-800">Galerie</h1>
      <select
        class="rounded bg-white p-4 text-gray-800 font-inter focus:outline-none"
        v-model="currentCategory"
      >
        <option value="all">Toutes les photos</option>
        <option value="wedding">Mariage</option>
        <option value="pregnancy">Grossesse</option>
        <option value="baby">Bébé</option>
        <option value="family">Famille</option>
        <option value="baptism">Baptême</option>
        <option value="couple">Couple</option>
      </select>
    </div>
    <div
      v-if="!!filteredImages.length"
      class="grid md:grid-cols-2 gap-4 md:gap-8"
    >
      <nuxt-img
        v-for="image in filteredImages"
        :src="image.url"
        :alt="image.cat"
        :key="image.url"
        @click.native="showModal(image.url)"
        class="object-cover h-64 w-full rounded transition transform hover:scale-105 hover:-rotate-1 cursor-pointer"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [
        {
          cat: "baby",
          url: "/img/img-0.jpeg",
        },
        {
          cat: "baptism",
          url: "/img/img-1.jpeg",
        },
        {
          cat: "family",
          url: "/img/img-2.jpeg",
        },
        {
          cat: "pregnancy",
          url: "/img/img-4.jpeg",
        },
        {
          cat: "wedding",
          url: "/img/img-5.jpeg",
        },
        {
          cat: "couple",
          url: "/img/img-3.jpeg",
        },
      ],
      isModalVisible: false,
      currentImage: null,
      currentCategory: "all",
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
          (image) => image.cat === this.currentCategory
        );

      return this.images;
    },
  },
  head: {
    title: "Galerie - Charles Cantin",
  },
};
</script>
