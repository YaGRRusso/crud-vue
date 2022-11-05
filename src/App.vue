<template>
  <div id="app">
    <c-modal
      :isModalOpen="isModalOpen"
      :handleCloseModal="handleCloseModal"
      :handleSubmitModal="handleSubmitModal"
    />
    <c-header :handleOpenModal="handleOpenModal" />
    <c-table :tableRows="usersList" />
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
      isModalOpen: false,
      usersList: UsersMockup,
    };
  },
  methods: {
    handleOpenModal() {
      this.isModalOpen = true;
    },
    handleCloseModal() {
      this.isModalOpen = false;
    },
    handleSubmitModal() {
      this.handleCloseModal();
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
  color: $dark-900;
}
</style>
