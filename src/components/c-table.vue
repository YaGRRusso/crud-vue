<template>
  <section class="table-container">
    <table class="table">
      <thead class="table__head table__head--desktop">
        <tr>
          <th
            v-for="(name, nameIndex) in tableHeaders"
            :key="'header' + nameIndex"
            v-show="nameIndex > 0"
          >
            {{ name }}
          </th>
          <th></th>
        </tr>
      </thead>
      <thead class="table__head table__head--mobile">
        <th>Informações</th>
        <th></th>
      </thead>
      <tbody class="table__body table__body--desktop">
        <tr v-for="(row, rowIndex) in tableRows" :key="'cell' + rowIndex">
          <td
            v-for="(cell, cellKey, cellIndex) in row"
            :key="'cell' + cellIndex"
            v-show="cellIndex > 0"
          >
            {{ cell }}
          </td>
          <td>
            <div class="table__buttons">
              <button @click="handleUpdate(row)" class="button button--sm">
                <edit-icon size="20" />
              </button>
              <button
                @click="handleDelete(row.id)"
                class="button button--error button--sm"
              >
                <trash-2-icon size="20" />
              </button>
            </div>
          </td>
        </tr>
      </tbody>
      <tbody class="table__body table__body--mobile">
        <tr v-for="(row, rowIndex) in tableRows" :key="'cell' + rowIndex">
          <td>
            <ul class="table__mobile-display">
              <li
                v-for="(cell, cellKey, cellIndex) in row"
                :key="'cell' + cellIndex"
                v-show="cellIndex > 0"
              >
                {{ cell }}
              </li>
            </ul>
          </td>
          <td>
            <div class="table__buttons">
              <button @click="handleUpdate" class="button button--sm">
                <edit-icon size="20" />
              </button>
              <button
                @click="handleDelete(row.id)"
                class="button button--error button--sm"
              >
                <trash-2-icon size="20" />
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang="ts">
import Vue from "vue";
import { EditIcon, Trash2Icon } from "vue-feather-icons";

export default Vue.extend({
  props: {
    tableHeaders: Array,
    tableRows: Array,
    handleDelete: Function,
    handleUpdate: Function,
  },
  components: {
    EditIcon,
    Trash2Icon,
  },
});
</script>

<style lang="scss" scoped>
@import "../styles/colors.scss", "../styles/components.scss";

.table-container {
  max-height: calc(100vh - 14rem);
  display: flex;
  margin-top: -4rem;
  background-color: var(--white);
  border-radius: 0.5rem;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 2px 8px;
  overflow: auto;
}

.table {
  width: 100%;
  border-collapse: collapse;

  &__head {
    th {
      border-bottom: 1px solid var(--light-100);
      text-align: left;
      padding: 1.75rem 0.75rem;
      margin-bottom: 1rem;
      color: var(--primary-500);
      font-size: 1.25rem;
      font-weight: 500;
    }

    &--mobile {
      display: none;
    }

    &--desktop {
      display: table-header-group;
    }

    @media (max-width: 1024px) {
      &--mobile {
        display: table-header-group;
      }

      &--desktop {
        display: none;
      }
    }
  }

  &__body {
    td {
      padding: 0.5rem 0.75rem;
    }

    tr {
      &:hover {
        background-color: var(--light-050);
      }
    }

    &--mobile {
      display: none;
      color: var(--dark-700);

      tr {
        &:nth-child(even) {
          background-color: var(--light-050);
        }
      }
    }

    &--desktop {
      display: table-row-group;
    }

    @media (max-width: 1024px) {
      &--mobile {
        display: table-row-group;
      }

      &--desktop {
        display: none;
      }
    }
  }

  &__mobile-display {
    margin: 0;
    padding: 0;
    list-style: none;

    li {
      max-width: calc(100vw - 10rem);
      overflow: hidden;
      text-overflow: ellipsis;

      &:nth-child(2) {
        font-weight: 500;
      }
    }
  }

  &__buttons {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 0.5rem;
  }
}
</style>
