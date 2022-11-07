<template>
  <header class="header">
    <div class="container">
      <div class="header__item">
        <img class="header__icon" src="../assets/logo.png" alt="logo" />
        <h1 class="header__title">Cadastro CRUD</h1>
      </div>
      <div class="header__item">
        <input
          v-model="searchValue"
          class="input"
          type="text"
          placeholder="Pesquisar..."
        />
        <button @click.self="handleOpenModal" class="button button--light">
          <plus-circle-icon
            stroke-width="1"
            stroke="#e3e3e3"
            fill="currentColor"
          />
          Novo
        </button>
      </div>
    </div>
  </header>
</template>

<script lang="ts">
import Vue from "vue";
import { PlusCircleIcon } from "vue-feather-icons";

export default Vue.extend({
  props: {
    handleOpenModal: Function,
    handleSearch: Function,
  },
  data() {
    return {
      searchValue: "",
    };
  },
  components: { PlusCircleIcon },
  watch: {
    searchValue(ev) {
      this.handleSearch(ev);
    },
  },
});
</script>

<style lang="scss" scoped>
@import "../styles/colors.scss", "../styles/components.scss";

.header {
  background-color: $primary-400;

  .container {
    min-height: 16rem;
    display: flex;
    padding-bottom: 4rem;
    justify-content: space-between;
    align-items: center;
    color: $light-100;

    @media (max-width: 768px) {
      gap: 0.5rem;
      padding-top: 2rem;
      padding-bottom: 6rem;
      flex-direction: column;
      justify-content: center;
    }
  }

  &__item {
    gap: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
  }

  &__icon {
    width: 3rem;
    height: 3rem;
  }

  &__title {
    font-size: 1.75rem;
    font-weight: 500;
  }
}
</style>
