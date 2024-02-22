<script setup lang="ts">
import UserList from "@/components/UserList.vue";
import UserDetail from "@/components/UserDetail.vue";
import { ref } from "vue";

const props = defineProps(["usersData"]);

const selectedUser = ref<any>({});

const handleUserSelected = (user: any) => {
  selectedUser.value = user;
};
</script>

<template>
  <main class="d-flex justify-content-between pt-5 h-85">
    <div class="w-50">
      <UserList
        :usersData="usersData"
        @userSelected="handleUserSelected"
      ></UserList>
    </div>
    <div class="w-75">
      <UserDetail :selectedUser="selectedUser"></UserDetail>
    </div>
  </main>
</template>

<style scoped>
.h-85 {
  height: 85%;
}
</style>
