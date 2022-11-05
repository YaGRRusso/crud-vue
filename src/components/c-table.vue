<template>
  <section class="table-container">
    <ul>
      <li v-for="(row, index) in tableRows" :key="index">
        {{ row }}
      </li>
    </ul>
  </section>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    tableRows: Array,
  },
});
</script>

<style lang="scss" scoped>
@import "../styles/colors.scss", "../styles/components.scss";

.table-container {
  height: calc(100vh - 16rem);
  display: flex;
  margin-top: -4rem;
  background-color: $white;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 2px 8px;
  overflow: auto;
}
</style>
