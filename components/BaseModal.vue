<template>
  <div
    class="fixed inset-0 bg-gray-800 bg-opacity-50 flex items-center justify-center z-50 p-5"
    @click="closeModal"
  >
    <slot />
  </div>
</template>

<script>
export default {
  emits: ["close-modal"],
  methods: {
    closeModal() {
      this.$emit("close-modal");
    },
  },
};
</script>
