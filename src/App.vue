<template>
  <div id="app">
    <c-modal
      :modalTitle="'Criar novo usuário'"
      :isModalOpen="isModalOpen"
      :handleCloseModal="handleCloseModal"
      :handleSubmitModal="handleSubmitModal"
      :modalInputs="modalInputs"
    />
    <c-modal
      :modalTitle="'Editar usuário'"
      :isModalOpen="isEditModalOpen"
      :handleCloseModal="handleCloseEditModal"
      :handleSubmitModal="handleSubmitEditModal"
      :modalInputs="editModalInputs"
    />
    <c-header
      :handleOpenModal="handleOpenModal"
      :handleSearch="handleSearchUsers"
      :darkMode="darkMode"
      :handleMode="handleChangeMode"
    />
    <c-table
      :handleDelete="handleDeleteUser"
      :handleUpdate="handleOpenEditModal"
      :tableRows="filteredUsersList"
      :tableHeaders="tableHeaders"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import CHeader from "./components/c-header.vue";
import CTable from "./components/c-table.vue";
import CModal from "./components/c-modal.vue";
import UsersMockup from "../mock/users";

export default Vue.extend({
  data() {
    return {
      darkMode: true,
      isModalOpen: false,
      isEditModalOpen: false,
      modalInputs: {
        name: { value: "", label: "Nome", type: "text", required: true },
        phone: { value: "", label: "Telefone", type: "text", required: true },
        address: { value: "", label: "Endereço", type: "text", required: true },
        email: { value: "", label: "Email", type: "text", required: true },
      },
      editModalInputs: {
        id: {
          value: 0,
          label: "Id",
          type: "text",
          required: true,
          disabled: true,
        },
        name: { value: "", label: "Nome", type: "text", required: true },
        phone: { value: "", label: "Telefone", type: "text", required: true },
        address: { value: "", label: "Endereço", type: "text", required: true },
        email: { value: "", label: "Email", type: "text", required: true },
      },
      usersList: UsersMockup,
      tableHeaders: ["Id", "Nome", "Telefone", "Endereço", "E-mail"],
      usersSearch: "",
    };
  },
  methods: {
    handleOpenModal() {
      this.isModalOpen = true;
    },
    handleChangeMode() {
      document.documentElement.classList.toggle("dark");
      this.darkMode = !this.darkMode;
    },
    handleOpenEditModal(user: any) {
      this.editModalInputs = {
        id: {
          value: user.id,
          label: "Id",
          type: "text",
          required: false,
          disabled: true,
        },
        name: { value: user.name, label: "Nome", type: "text", required: true },
        phone: {
          value: user.phone,
          label: "Telefone",
          type: "text",
          required: true,
        },
        address: {
          value: user.address,
          label: "Endereço",
          type: "text",
          required: true,
        },
        email: {
          value: user.email,
          label: "Email",
          type: "text",
          required: true,
        },
      };
      this.isEditModalOpen = true;
    },
    handleCloseModal() {
      this.isModalOpen = false;
    },
    handleCloseEditModal() {
      this.isEditModalOpen = false;
    },
    handleSearchUsers(value: string) {
      this.usersSearch = value;
    },
    resetModalInputs() {
      this.modalInputs = {
        name: { value: "", label: "Nome", type: "text", required: true },
        phone: { value: "", label: "Telefone", type: "text", required: true },
        address: { value: "", label: "Endereço", type: "text", required: true },
        email: { value: "", label: "Email", type: "email", required: true },
      };
    },
    handleSubmitModal() {
      const newUser = {
        id: this.usersList.length + 1,
        name: this.modalInputs.name.value,
        phone: this.modalInputs.phone.value,
        address: this.modalInputs.address.value,
        email: this.modalInputs.email.value,
      };
      this.usersList.push(newUser);
      this.resetModalInputs();
      this.handleCloseModal();
    },
    handleSubmitEditModal() {
      const editIndex = this.usersList.findIndex(
        (item) => item.id === this.editModalInputs.id.value
      );
      const newValue = {
        id: this.editModalInputs.id.value,
        name: this.editModalInputs.name.value,
        phone: this.editModalInputs.phone.value,
        address: this.editModalInputs.address.value,
        email: this.editModalInputs.email.value,
      };
      Vue.set(this.usersList, editIndex, newValue);
      this.handleCloseEditModal();
    },
    handleDeleteUser(id: number) {
      const newList = this.usersList.filter((item) => item.id !== id);
      this.usersList = newList;
    },
  },
  computed: {
    filteredUsersList(): unknown[] {
      if (this.usersSearch) {
        const filteredList = this.usersList.filter(
          (item) =>
            item.name.toLowerCase().includes(this.usersSearch.toLowerCase()) ||
            item.phone.toLowerCase().includes(this.usersSearch.toLowerCase()) ||
            item.address
              .toLowerCase()
              .includes(this.usersSearch.toLowerCase()) ||
            item.email.toLowerCase().includes(this.usersSearch.toLowerCase())
        );
        return filteredList;
      } else {
        return this.usersList;
      }
    },
  },
  components: {
    CHeader,
    CTable,
    CModal,
  },
});
</script>

<style lang="scss">
@import "./styles/colors.scss";
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&display=swap");
body {
  margin: 0;
  padding: 0;
  padding-bottom: 2rem;
  color: var(--dark-900);
  background-color: var(--white);
}
</style>
