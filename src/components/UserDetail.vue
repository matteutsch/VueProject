<script lang="ts">
import { updateUser, deleteUser, createUser } from "../services/ApiService.vue";

export default {
  props: {
    selectedUser: {
      type: Object,
      default: () => [],
      required: true,
    },
  },

  data() {
    return {
      firstNameInput: null as HTMLInputElement | null,
      lastNameInput: null as HTMLInputElement | null,
      emailInput: null as HTMLInputElement | null,
      isActive: false,
      isCreating: false,

      updatedUserData: {
        id: this.selectedUser.id,
        email: this.selectedUser.email,
        first_name: this.selectedUser.first_name,
        last_name: this.selectedUser.last_name,
        avatar: this.selectedUser.avatar,
      },

      newUserData: {
        id: 32,
        email: "matthias.teutsch@freenet.de",
        first_name: "Matthias",
        last_name: "Teutsch",
        avatar: "",
      },
    };
  },
  watch: {
    selectedUser(newVal) {
      if (newVal && Object.keys(newVal).length > 0) {
        this.isCreating = false;
        this.isActive = false;
      }
    },
  },
  methods: {
    async submitForm() {
      this.toggleInput();
      await this.updateUser();
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

    async addNewUser() {
      try {
        const newUser = await createUser(this.newUserData);
        console.log("newUser", newUser);
        this.clearForm();
      } catch (error) {
        console.error(error);
      }
    },

    /**
     * @description Clears the form values and sets the mode to create
     */
    clearForm() {
      if (this.$refs.firstNameInput) {
        (this.$refs.firstNameInput as HTMLInputElement).value = "";
      }
      if (this.$refs.lastNameInput) {
        (this.$refs.lastNameInput as HTMLInputElement).value = "";
      }
      if (this.$refs.emailInput) {
        (this.$refs.emailInput as HTMLInputElement).value = "";
      }
      this.setCreateMode();
    },
    /**
     * @description sets booleans to change the style of the form
     */
    setCreateMode() {
      this.isCreating = true;
      this.isActive = true;
    },
  },
};
</script>

<!-- --------------------------------------------------------------- -->

<template>
  <i
    @click="clearForm()"
    class="fs-2 add-icon text-primary bi bi-person-fill-add opacity-50 position-absolute top-0 end-0 me-5 mt-5"
  ></i>

  <div
    class="d-flex h-100 align-items-center"
    v-if="Object.keys(selectedUser).length > 0 || isCreating"
  >
    <div class="d-flex justify-content-around w-100">
      <div class="align-self-sm-start">
        <img
          v-if="!isCreating && selectedUser.avatar !== ''"
          style="width: 160px; height: 160px"
          class="rounded-circle img-thumbnail"
          :src="selectedUser.avatar"
          alt="User Avatar"
        />

        <i v-else style="font-size: 160px" class="bi bi-person-circle"></i>
      </div>

      <!-- outsource form -->
      <form @submit.prevent="submitForm" class="w-50">
        <label class="text-secondary mb-1" for="firstName">Vorname:</label>
        <input
          ref="firstNameInput"
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
          ref="lastNameInput"
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
          ref="emailInput"
          class="form-control mb-4 border-0 bg-input"
          type="email"
          id="email"
          v-model="selectedUser.email"
          :class="{ 'bg-input-active': isActive }"
          :disabled="!isActive"
        />

        <div v-if="!isCreating">
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
        </div>

        <div v-else>
          <button
            title="Nutzer Hinzufügen"
            class="btn btn-primary rounded-circle"
            @click="addNewUser()"
          >
            <i class="bi bi-person-fill-add"></i>
          </button>
        </div>
      </form>
    </div>
  </div>
  <div v-else class="fs-2 d-flex justify-content-start align-items-center">
    <i class="arrow-animation bi bi-arrow-left me-4"></i>Wähle einen Nutzer aus
    der Liste
  </div>
</template>

<!-- --------------------------------------------------------------- -->

<style scoped>
.arrow-animation {
  animation: breathe 0.5s infinite alternate;
}

@keyframes breathe {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-5px);
  }
}
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
