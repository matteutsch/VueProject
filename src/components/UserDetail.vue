<script lang="ts">
import { updateUser, deleteUser } from "../services/ApiService.vue";

export default {
  props: {
    selectedUser: {
      type: Object,
      default: () => [],
      required: true,
    },
  },
  mode: {
    type: String,
    default: "edit",
  },
  data() {
    return {
      isActive: false,

      updatedUserData: {
        id: this.selectedUser.id,
        email: this.selectedUser.email,
        first_name: this.selectedUser.first_name,
        last_name: this.selectedUser.last_name,
        avatar: this.selectedUser.avatar,
      },
    };
  },
  methods: {
    async submitForm() {
      await this.updateUser();
      this.toggleInput();
    },
    toggleInput() {
      this.isActive = !this.isActive;
    },

    async updateUser() {
      try {
        const updatedUser = await updateUser(
          this.selectedUser.id,
          this.updatedUserData
        );
        console.log("updatedUser", updatedUser);
      } catch (error) {
        console.error(error);
      }
    },

    async deleteUser() {
      try {
        const deletedUser = await deleteUser(this.selectedUser.id);
        console.log("deletedUser", deletedUser);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<!-- --------------------------------------------------------------- -->

<template>
  <i
    class="fs-2 add-icon text-primary bi bi-person-fill-add opacity-50 position-absolute top-0 end-0 me-5 mt-5"
  ></i>

  <div
    class="d-flex h-100 align-items-center"
    v-if="Object.keys(selectedUser).length > 0"
  >
    <div class="d-flex justify-content-around w-100">
      <div class="align-self-sm-start">
        <img
          style="width: 160px; height: 160px"
          class="rounded-circle img-thumbnail"
          :src="selectedUser.avatar"
          alt="User Avatar"
        />
      </div>

      <!-- outsource form -->
      <form @submit.prevent="submitForm" class="w-50">
        <label class="text-secondary mb-1" for="firstName">Vorname:</label>
        <input
          class="form-control mb-4 border-0 bg-input"
          type="text"
          id="firstName"
          v-model="selectedUser.first_name"
          :class="{
            'is-invalid': selectedUser.first_name == '',
            'bg-input-active': isActive,
          }"
          required
          :disabled="!isActive"
        />
        <label class="text-secondary mb-1" for="lastName">Nachname:</label>
        <input
          class="form-control mb-4 border-0 bg-input"
          type="text"
          id="lastName"
          v-model="selectedUser.last_name"
          :class="{
            'is-invalid': selectedUser.last_name === '',
            'bg-input-active': isActive,
          }"
          required
          :disabled="!isActive"
        />

        <label class="text-secondary mb-1" for="email">Email:</label>
        <input
          class="form-control mb-4 border-0 bg-input"
          type="email"
          id="email"
          v-model="selectedUser.email"
          :class="{ 'bg-input-active': isActive }"
          :disabled="!isActive"
        />

        <button
          class="rounded-circle btn btn-primary opacity-75"
          @click="toggleInput()"
          v-if="!isActive"
          title="Bearbeiten"
        >
          <i class="bi bi-pencil"></i>
        </button>
        <div class="d-flex justify-content-between" v-else>
          <div>
            <button
              type="submit"
              class="rounded-circle btn btn-success me-4"
              title="Speichern"
            >
              <i class="bi bi-floppy"></i>
            </button>
            <button
              title="Abbrechen"
              class="rounded-circle btn btn-outline-warning"
              @click="toggleInput()"
            >
              <i class="bi bi-x-circle"></i>
            </button>
          </div>
          <button
            class="rounded-circle btn btn-outline-danger"
            title="Löschen"
            @click="deleteUser()"
          >
            <i class="bi bi-person-dash"></i>
          </button>
        </div>
      </form>
    </div>
  </div>
  <div v-else>kein User ausgewählt</div>
</template>

<!-- --------------------------------------------------------------- -->

<style scoped>
input:focus {
  outline: none;
  box-shadow: inset 5px 5px 10px rgba(0, 0, 0, 0.2) !important;
}
.bg-input {
  background: linear-gradient(to left, transparent, #cfe2ff);
}
.bg-input-active {
  background: linear-gradient(to left, transparent, #cff4fc);
}

.add-icon {
  transition: all 0.225s ease-in-out;
}
.add-icon:hover {
  transform: scale(1.05);
  cursor: pointer;
  opacity: 1 !important;
}
</style>
