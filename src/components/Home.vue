<script setup lang="ts"></script>

<template>
  <div class="text-secondary-emphasi w-100 fs-5 mt-5 ms-5">
    <p class="w-50 text-start">
      Herzlich willkommen!
      <br />
      <br />
      Mit dieser User-Management-Applikation hast du die Kontrolle über all
      deine App-Nutzer.
      <br />Du kannst ihre <span class="text-purple">Daten einsehen</span>,
      <span class="text-success">bearbeiten</span>,
      <span class="text-danger text-opacity-75">löschen</span> oder neue
      Benutzer <span class="text-primary text-opacity-75">hinzufügen</span>.
      <br />
      Entdecke die Möglichkeiten:
    </p>
    <p class="text-start">
      <RouterLink
        class="btn btn-lg btn-outline-primary fs-2 px-5 me-5"
        to="/user"
        >Zu deinen Usern</RouterLink
      >
    </p>
  </div>
</template>

<style scoped>
.text-purple {
  color: #6f42c1;
}
</style>
