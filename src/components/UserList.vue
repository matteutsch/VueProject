<script lang="ts">
import UserItem from "@/components/UserItem.vue";
import { isArrayLiteralExpression } from "typescript";

export default {
  components: {
    UserItem,
  },
  props: {
    usersData: {
      type: Object,
      default: () => [],
      required: true,
    },
  },
  methods: {
    selectUser(user: any) {
      this.$emit("userSelected", user);
    },
  },
};
</script>

<template>
  <div
    class="bg-primary-subtle rounded-4 w-75 list-shadow py-4 h-100 overflow-y"
  >
    <div>
      <UserItem
        v-for="user in usersData"
        :key="user.id"
        :user="user"
        @click="selectUser(user)"
      ></UserItem>
    </div>
  </div>
</template>

<style scoped>
.list-shadow {
  box-shadow: inset 0 10px 10px rgba(0, 0, 0, 0.2);
  contain: content;
  max-width: 400px;
}
.overflow-y {
  overflow-y: auto;
  overflow-x: hidden;
}
::-webkit-scrollbar {
  display: none;
}
</style>
