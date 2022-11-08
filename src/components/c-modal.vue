<template>
  <div
    v-if="isModalOpen"
    class="modal-background"
    @click.self="handleCloseModal"
  >
    <div class="modal">
      <div class="modal__header">
        <span class="modal__title">{{ modalTitle }}</span>
        <x-icon @click.self="handleCloseModal" class="modal__close" />
      </div>
      <form @submit.prevent="handleSubmitModal">
        <div class="modal__body">
          <label
            class="modal__label"
            v-for="(input, inputKey, inputIndex) in modalInputs"
            :key="'input' + inputIndex"
          >
            <span class="modal__label-text">
              {{ input.label }}
            </span>
            <input
              class="modal__input"
              v-model="input.value"
              placeholder="placeholder"
              :type="input.type"
              :required="input.required"
              :disabled="input.disabled"
            />
          </label>
        </div>
        <div class="modal__footer">
          <button
            type="button"
            @click.self="handleCloseModal"
            class="button button--error"
          >
            Cancelar
          </button>
          <input type="submit" class="button button--primary" value="Salvar" />
        </div>
      </form>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { XIcon } from "vue-feather-icons";

export default Vue.extend({
  props: {
    modalTitle: String,
    isModalOpen: Boolean,
    handleCloseModal: Function,
    handleSubmitModal: Function,
    modalInputs: Object,
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
  z-index: 5;
}

.modal {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: stretch;
  background-color: var(--white);
  width: 90vw;
  max-width: 30rem;
  border-radius: 0.5rem;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 2px 8px;
  overflow: hidden;

  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: var(--primary-400);
    padding: 2rem 1rem;
    color: var(--light-100);
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
    flex-direction: column;
    flex: 1;
    padding: 2rem 1rem;
    gap: 1.5rem;
  }

  &__label {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-direction: column;
    gap: 0.25rem;
    width: 100%;
    max-width: 25rem;
  }

  &__label-text {
    font-weight: 500;
    color: var(--primary-400);
  }

  &__input {
    width: 100%;
    border: none;
    background-color: transparent;
    border-bottom: 2px solid var(--primary-300);
    padding: 0.5rem 0;
    margin-top: -2rem;
    transition: all 200ms;
    outline: none;
    color: var(--black);

    &::placeholder {
      color: transparent;
    }

    &:active,
    &:focus,
    &:not(:placeholder-shown) {
      margin-top: 0;
    }
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
