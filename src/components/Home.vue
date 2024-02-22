<script setup lang="ts"></script>

<template>
  <div class="text-secondary-emphasi w-100 fs-5 pt-5 ps-5 h-100 bg-image">
    <p style="width: 40%" class="text-start">
      Herzlich willkommen!
      <br />
      <br />
      Mit dieser User-Management-Applikation hast du die Kontrolle über all
      deine App-Nutzer.
      <br />Du kannst<br />
      -ihre
      <span class="text-primary text-opacity-75">Daten einsehen</span>,<br />
      -<span class="text-primary text-opacity-75">bearbeiten</span>,<br />
      -<span class="text-primary text-opacity-75">löschen</span><br />
      -oder neue Benutzer
      <span class="text-primary text-opacity-75">hinzufügen</span>.
      <br />
      <br />
      Entdecke die Möglichkeiten:
    </p>
    <RouterLink class="btn btn-lg btn-outline-primary fs-3 px-5 mt-4" to="/user"
      >Zur Übersicht</RouterLink
    >
  </div>
</template>

<style scoped>
.bg-image {
  background-image: url("src/assets/landing.jpg");
  background-size: 50% 75%;
  background-position-y: 33%;
  background-position-x: 100%;
  background-repeat: no-repeat;
}
</style>
