<script setup lang="ts">
import { RouterView } from "vue-router";
import "bootstrap-icons/font/bootstrap-icons.css";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

import { onMounted, ref } from "vue";
import { getAllUsers } from "./services/ApiService.vue";

let usersData = ref<Object[]>([]);
onMounted(async () => {
  try {
    usersData.value = await getAllUsers();
  } catch (error) {
    console.error("Fehler beim Abrufen der Benutzerdaten:", error);
  }
});
</script>

<template>
  <div class="d-flex flex-column justify-content-between h-f">
    <div class="p-4 h-100">
      <Header></Header>
      <RouterView :usersData="usersData" />
    </div>
    <Footer></Footer>
  </div>
</template>

<style scoped>
.h-f {
  height: calc(100% - 24px);
}
</style>
