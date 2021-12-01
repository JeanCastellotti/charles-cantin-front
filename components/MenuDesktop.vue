<template>
  <div>
    <NuxtLink
      to="/"
      class="flex items-center space-x-2 transition transform hover:scale-105"
    >
      <IconHome class="h-5 w-5" :class="iconStyle" />
      <span class="text-gray-400 font-nunito tracking-wider font-black text-lg"
        >Accueil</span
      >
    </NuxtLink>
    <NuxtLink
      to="/gallery"
      class="flex items-center space-x-2 transition transform hover:scale-105"
    >
      <IconGrid class="h-5 w-5" :class="iconStyle" />
      <span class="text-gray-400 font-nunito tracking-wider font-black text-lg"
        >Galerie</span
      >
    </NuxtLink>
    <NuxtLink
      to="/prices"
      class="flex items-center space-x-2 transition transform hover:scale-105"
    >
      <IconTag class="h-5 w-5" :class="iconStyle" />
      <span class="text-gray-400 font-nunito tracking-wider font-black text-lg"
        >Tarifs</span
      >
    </NuxtLink>
    <NuxtLink
      to="/contact"
      class="flex items-center space-x-2 transition transform hover:scale-105"
    >
      <IconEnvelop class="h-5 w-5" :class="iconStyle" />
      <span class="text-gray-400 font-nunito tracking-wider font-black text-lg"
        >Contact</span
      >
    </NuxtLink>
  </div>
</template>

<script>
export default {
  props: ["iconStyle"],
};
</script>
