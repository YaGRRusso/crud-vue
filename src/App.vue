<template>
  <div id="app">
    <c-header />
    <c-table />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import CHeader from "./components/c-header.vue";
import CTable from "./components/c-table.vue";

export default Vue.extend({
  data() {
    return {};
  },
  components: {
    CHeader,
    CTable,
  },
});
</script>

<style lang="scss">
@import "./styles/colors.scss";
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&display=swap");
body {
  margin: 0;
  padding: 0;
}
</style>
