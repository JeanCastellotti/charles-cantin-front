<template>
  <div>
    <h1 class="font-neucha text-5xl text-gray-800 mb-5">Contact</h1>
    <div
      v-if="error"
      class="bg-red-400 text-white rounded p-5 mb-5 flex items-center justify-center space-x-5"
    >
      <div class="rounded-full bg-red-500 h-12 w-12 flex">
        <IconX class="h-8 w-8 text-white m-auto" />
      </div>
      <p class="font-inter">Les informations saisies sont incorrectes.</p>
    </div>
    <div
      v-if="formIsValid"
      class="rounded bg-green-400 text-white flex items-center justify-center p-5 space-x-5 mb-5"
    >
      <div class="rounded-full bg-green-500 h-12 w-12 flex">
        <IconCheck class="h-8 w-8 text-white m-auto" />
      </div>
      <p class="font-inter">Votre message a bien été envoyé.</p>
    </div>
    <form @submit.prevent="submitForm" autocomplete="off">
      <div class="mb-3">
        <label for="email" class="mb-1 block text-gray-500 font-inter text-lg"
          >Adresse e-mail</label
        >
        <input
          type="text"
          id="email"
          v-model.trim="email"
          class="rounded border-2 border-gray-400 p-4 w-full font-inter text-gray-400 focus:outline-none"
        />
      </div>
      <div class="mb-3">
        <label for="message" class="mb-1 block text-gray-500 font-inter text-lg"
          >Message</label
        >
        <textarea
          id="message"
          v-model.trim="message"
          required
          class="resize-none rounded border-2 border-gray-400 p-4 h-56 w-full font-inter text-gray-400 focus:outline-none"
        ></textarea>
      </div>
      <button
        class="transition rounded p-4 w-full bg-gray-700 text-gray-50 font-neucha text-2xl hover:bg-gray-800"
      >
        Envoyer
      </button>
    </form>
  </div>
</template>

<script>
import * as EmailValidator from "email-validator";

export default {
  data() {
    return {
      email: "",
      message: "",
      error: null,
      formIsValid: false,
    };
  },
  methods: {
    submitForm() {
      this.error = null;
      this.formIsValid = false;

      const isEmailValid = EmailValidator.validate(this.email);
      console.log(isEmailValid);

      if ((!this.email && !isEmailValid) || !this.message) {
        this.error = true;
        return;
      }

      this.formIsValid = true;

      this.email = "";
      this.message = "";
    },
  },
};
</script>
