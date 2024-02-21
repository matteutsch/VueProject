<script setup lang="ts">
import UserList from "@/components/UserList.vue";
import UserDetail from "@/components/UserDetail.vue";
</script>

<template class="h-100">
  <main class="d-flex justify-content-between mt-4 h-85">
    <div class="w-50">
      <UserList></UserList>
    </div>
    <div class="w-50">
      <UserDetail></UserDetail>
    </div>
  </main>
</template>

<style scoped>
.h-85 {
  height: 85%;
}
</style>
