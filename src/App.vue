<script setup lang="ts">
import { RouterView } from "vue-router";
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import "bootstrap-icons/font/bootstrap-icons.css";
import { BootstrapVue } from "bootstrap-vue";

import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

import { onMounted } from "vue";
import { getAllUsers } from "./services/ApiService.vue";

/* onMounted(async () => {
  try {
    const usersData = await getAllUsers();
    console.log(usersData);
  } catch (error) {
    console.error("Fehler beim Abrufen der Benutzerdaten:", error);
  }
}); */
</script>

<template>
  <div class="d-flex flex-column justify-content-between h-100">
    <div class="p-4 h-100">
      <Header></Header>
      <RouterView />
    </div>
    <Footer></Footer>
  </div>
</template>

<style scoped></style>
