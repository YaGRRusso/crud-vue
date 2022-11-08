<template>
  <header class="header">
    <div class="container">
      <div class="header__item">
        <img class="header__icon" src="../assets/logo.png" alt="logo" />
        <div class="header__group">
          <h1 class="header__title">Cadastro CRUD</h1>
          <span class="header__theme" v-if="darkMode" @click="handleMode"
            ><moon-icon fill="currentColor"
          /></span>
          <span class="header__theme" v-if="!darkMode" @click="handleMode"
            ><sun-icon fill="currentColor"
          /></span>
        </div>
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
import { PlusCircleIcon, MoonIcon, SunIcon } from "vue-feather-icons";

export default Vue.extend({
  props: {
    handleOpenModal: Function,
    handleSearch: Function,
    handleMode: Function,
    darkMode: Boolean,
  },
  data() {
    return {
      searchValue: "",
    };
  },
  components: { PlusCircleIcon, MoonIcon, SunIcon },
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
  background-color: var(--primary-400);

  .container {
    min-height: 16rem;
    display: flex;
    padding-bottom: 4rem;
    justify-content: space-between;
    align-items: center;
    color: var(--light-100);

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

  &__group {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 0.5rem;
  }

  &__theme {
    cursor: pointer;
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
