<template>
  <nav>
    <div class="space-y-8 flex flex-col items-center">
      <NuxtLink
        to="/"
        class="font-neucha text-gray-300 text-4xl"
        @click.native="closeMenu"
        >Accueil</NuxtLink
      >
      <NuxtLink
        to="/gallery"
        class="font-neucha text-gray-300 text-4xl"
        @click.native="closeMenu"
        >Galerie</NuxtLink
      >
      <NuxtLink
        to="/prices"
        class="font-neucha text-gray-300 text-4xl"
        @click.native="closeMenu"
        >Tarifs</NuxtLink
      >
      <NuxtLink
        to="/contact"
        class="font-neucha text-gray-300 text-4xl"
        @click.native="closeMenu"
        >Contact</NuxtLink
      >
    </div>
    <IconArrowNarrowLeft
      class="absolute right-5 bottom-5 h-8 w-8 m-auto text-gray-400"
      @click.native="closeMenu"
    />
  </nav>
</template>

<script>
export default {
  emits: ["close-menu"],
  methods: {
    closeMenu() {
      this.$emit("close-menu");
    },
  },
};
</script>
