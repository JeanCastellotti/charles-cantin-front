<template>
  <header class="max-w-screen-lg m-auto" :class="headerStyle">
    <nav class="flex justify-between items-center px-4">
      <MenuDesktop class="space-x-8 hidden md:flex" :iconStyle="iconStyle" />
      <IconMenu
        class="h-8 w-8 md:hidden"
        :class="iconStyle"
        @click.native="showMenuMobile"
      />
      <div class="flex space-x-4">
        <a href="#">
          <IconFacebook class="h-7 w-7 text-blue-500" />
        </a>
        <a href="#">
          <IconInstagram class="h-7 w-7 text-pink-500" />
        </a>
      </div>
    </nav>
    <transition name="menu">
      <MenuMobile
        v-show="isMenuMobileVisible"
        @close-menu="closeMenuMobile"
        class="fixed inset-0 bg-gray-800 z-50 px-12 flex flex-col items-center justify-around md:hidden"
      />
    </transition>
  </header>
</template>

<script>
export default {
  props: {
    theme: {
      type: String,
      required: false,
      default: "light",
    },
  },
  data() {
    return {
      isMenuMobileVisible: false,
    };
  },
  methods: {
    showMenuMobile() {
      this.isMenuMobileVisible = true;
    },
    closeMenuMobile() {
      this.isMenuMobileVisible = false;
    },
  },
  computed: {
    iconStyle() {
      if (this.theme === "dark") {
        return "text-gray-200";
      }

      return ["text-gray-500"];
    },
    headerStyle() {
      if (this.theme === "light") {
        return ["pb-5", "mb-7", "border-b", "border-gray-200"];
      }
    },
  },
};
</script>
