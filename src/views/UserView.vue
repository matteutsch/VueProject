<script setup lang="ts">
import UserList from "@/components/UserList.vue";
import UserDetail from "@/components/UserDetail.vue";
import { onMounted, ref } from "vue";

const props = defineProps(["usersData"]);

onMounted(() => {
  console.log("props.userData in UserView.vue:", props.usersData);
});

const selectedUser = ref<any>({});

const handleUserSelected = (user: any) => {
  selectedUser.value = user;
  console.log("selectedUser.value", selectedUser.value);
};
</script>

<template class="h-100">
  <main class="d-flex justify-content-between mt-4 h-85">
    <div class="w-50">
      <UserList
        :usersData="usersData"
        @userSelected="handleUserSelected"
      ></UserList>
    </div>
    <div class="w-50">
      <UserDetail :selectedUser="selectedUser"></UserDetail>
    </div>
  </main>
</template>

<style scoped>
.h-85 {
  height: 85%;
}
</style>
