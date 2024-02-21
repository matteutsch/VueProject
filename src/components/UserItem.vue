<script lang="ts">
export default {
  props: {
    user: {
      type: Object,
      required: true,
    },
  },
};
</script>

<template>
  <div class="px-5 py-2 text-start list-item w-100 fs-5">
    <img
      style="
         {
          width: 48px;
          height: 48px;
        }
      "
      class="rounded-circle me-4"
      :src="user.avatar"
      alt="User Avatar"
    />
    <span>{{ user.first_name }} {{ user.last_name }} </span>
  </div>
</template>

<style scoped>
.list-item {
  transition: all 0.225s ease-in-out;
}
.list-item:hover {
  transform: scale(1.05);
  cursor: pointer;
  color: #0d6efd;
  font-weight: bold;
}
</style>
