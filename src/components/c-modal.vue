<template>
  <div
    v-if="isModalOpen"
    class="modal-background"
    @click.self="handleCloseModal"
  >
    <div class="modal">
      <div class="modal__header">
        <span class="modal__title">Title</span>
        <x-icon @click.self="handleCloseModal" class="modal__close" />
      </div>
      <div class="modal__body">Body</div>
      <div class="modal__footer">
        <button @click.self="handleCloseModal" class="button button--error">
          Cancelar
        </button>
        <button @click.self="handleSubmitModal" class="button button--primary">
          Salvar
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { XIcon } from "vue-feather-icons";

export default Vue.extend({
  props: {
    isModalOpen: Boolean,
    handleCloseModal: Function,
    handleSubmitModal: Function,
  },
  components: {
    XIcon,
  },
});
</script>

<style lang="scss" scoped>
@import "../styles/colors.scss", "../styles/components.scss";

.modal-background {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-color: #00000050;
}

.modal {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: stretch;
  background-color: $light-100;
  min-width: 60vw;
  max-width: 800px;
  min-height: 75vh;
  max-height: 800px;
  border-radius: 0.5rem;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 2px 8px;
  overflow: hidden;

  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: $primary-400;
    padding: 1rem;
    color: $light-100;
    font-weight: 600;
  }

  &__title {
    font-size: 1.5rem;
  }

  &__close {
    cursor: pointer;
  }

  &__body {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 1;
    padding: 1rem;
    gap: 1rem;
  }

  &__footer {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 1rem;
    padding: 1rem;
  }
}
</style>
