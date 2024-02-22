<script lang="ts">
export default {
  props: {
    selectedUser: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      formData: {
        name: "",
        email: "",
      },
    };
  },
  methods: {
    submitForm() {
      console.log("Form submitted with data:");
    },
  },
};
</script>

<template>
  <div class="fs-1 d-flex align-items-center mb-4">
    <img
      style="width: 80px; height: 80px"
      class="rounded-circle me-4"
      :src="selectedUser.avatar"
      alt="User Avatar"
    />
    <span>{{ selectedUser.first_name }} {{ selectedUser.last_name }}</span>
  </div>

  <form @submit.prevent="submitForm">
    <label for="name">FirstName:</label>
    <input
      class="form-control"
      type="text"
      id="firstName"
      v-model="selectedUser.first_name"
      :class="{ 'is-invalid': selectedUser.first_name == '' }"
      required
    />
    <label for="name">LastName:</label>
    <input
      class="form-control"
      type="text"
      id="lastName"
      v-model="selectedUser.last_name"
      :class="{ 'is-invalid': selectedUser.last_name === '' }"
      required
    />

    <label for="email">Email:</label>
    <input
      class="form-control"
      type="email"
      id="email"
      v-model="selectedUser.email"
    />

    <button
      :disabled="
        selectedUser.last_name === '' || selectedUser.first_name === ''
      "
      class="btn btn-primary"
      type="submit"
    >
      Submit
    </button>
  </form>
</template>
