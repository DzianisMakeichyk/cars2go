<template>
  <div>
    <p>Add item</p>
    <section>
      <label label="Title">
        <input type="text" v-model="title" placeholder="title" />
      </label>
    </section>
    
    <button @click="close">
      Close
    </button>
    <button @click="additem">
      Save
    </button>
  </div>
</template>

<script>
export default {
  name: "AddModal",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    additem() {
      const payload = {
        title: this.title
      };
      this.$emit("add-item", payload);
    },
    close() {
      this.$emit("close-item");
    }
  }
};
</script>

<style scoped></style>