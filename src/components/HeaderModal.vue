<template>
  <header>
    <h1>{{ title }}</h1>


    <button @click="$emit('handle-modal-active', true)">
      Add
    </button>
  </header>
</template>

<script>
export default {
  name: "HeaderModal",
  props: {
    title: {
      type: String,
      default: "Cars2go"
    }
  },
};
</script>

<style scoped lang="scss"></style>