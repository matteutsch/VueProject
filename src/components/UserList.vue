<script lang="ts">
import UserItem from "@/components/UserItem.vue";
export default {
  components: {
    UserItem,
  },
};
</script>

<template>
  <div class="bg-primary-subtle rounded-4 w-75 list-shadow py-4 h-100">
    <div>
      <UserItem></UserItem>
    </div>
  </div>
</template>

<style scoped>
.list-shadow {
  box-shadow: inset 0 10px 10px rgba(0, 0, 0, 0.2);
  contain: content;
}
</style>
