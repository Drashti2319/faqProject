<template>
  <v-app>
    <div class="d-flex justify-center align-center">
      <faq />
      <snackbar
        v-model="showToastMessage"
        :color="snackBarColor"
        :message="snackbarMessage"
      />
    </div>
  </v-app>
</template>

<script>
import Faq from "./components/faq.vue";
import {bus} from "@/main"
import Snackbar from './components/snackbar.vue';

export default {
  name: "App",

  components: {
    Faq,
    Snackbar,
  },

  data: () => ({
    showToastMessage: false,
    snackBarColor: "primary",
    snackbarMessage: "",
  }),
  mounted() {
    bus.$on("showToastMessage", ({ color, message }) => {
      this.snackBarColor = color;
      this.snackbarMessage = message;
      this.showToastMessage = true;
    });
  },
  beforeDestroy() {
    bus.$off("showToastMessage");
  },
};
</script>
