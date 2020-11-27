<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-search></todo-search>
    <todo-table></todo-table>
  </div>
</template>

<script>
import TodoTable from "@/components/TableModal.vue";
import TodoSearch from "@/components/SearchModal.vue";
import TodoHeader from "@/components/SearchModal.vue";

export default {
  name: 'app',
  components: {
    TodoTable,
    TodoSearch,
    TodoHeader,
  }
}
</script>

<style lang="scss">
</style>
