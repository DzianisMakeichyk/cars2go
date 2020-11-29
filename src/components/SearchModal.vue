<template>
  <div class="search">
    <div class="search__input">
      <label for="search">🔍</label>
      <input
        type="text"
        placeholder="Search"
        name="search"
        v-model="value"
      />
    </div>

    <button class="button__secondary" @click="submitSearch">Search</button>
  </div>
</template>

<script>
export default {
  name: 'SearchModal',

  data: () => ({
    value: '',
    items: [],
  }),

  mounted() {
    if (localStorage.getItem("items")) {
      this.items = JSON.parse(localStorage.getItem("items"));
    }
  },

  methods: {
    submitSearch() {
      const { value, items } = this;
      const searchValue = value.toLowerCase();
      let searchItems = [];

      searchItems = items
        .filter(item => items.length > 0 ? item.title.toLowerCase().includes(searchValue) : item)

      this.$emit("search-items", searchItems);
    }
  }
}
</script>

<style lang="scss" scoped>
  .search {
    padding: 20px 30px;
    display: flex;
    justify-content: space-between;
    align-content: center;
  }

  .search__input {
    width: 100%;
    margin-right: 35px;
    position: relative;

    input {
      font-weight: 15px;
      width: 100%;
      padding: 7px 10px;
      border-radius: 5px;
      border: 1px solid $wildSand;
      line-height: 1;
      box-sizing: border-box;
      padding-left: 40px;

      &::placeholder {
        color: $silverChalice;
      }
    }

    label {
      position: absolute;
      left: 10px;
      top: 8px;
    }
  }
</style>