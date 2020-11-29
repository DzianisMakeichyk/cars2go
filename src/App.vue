<template>
  <div id="app">
    <header-modal
      @handle-modal-active="handleModalActive"
    ></header-modal>
    <search-modal
      :items="items"
      @search-items="searchItems"
    ></search-modal>
    <table-modal
      :items="items"
      @delete-item="deleteitem"
    >
    </table-modal>

  <transition name="fade">
    <add-modal
      v-if="isAddModalActive"
      @add-item="onAdditem"
      @close-item="onClose"
    ></add-modal>
    </transition>
  </div>
</template>

<script>
import TableModal from "@/components/TableModal";
import SearchModal from "@/components/SearchModal";
import HeaderModal from "@/components/HeaderModal";
import AddModal from "@/components/AddModal";

export default {
  name: 'app',
  components: {
    TableModal,
    SearchModal,
    HeaderModal,
    AddModal,
  },
  data() {
    return {
      items: [],
      isAddModalActive: false
    };
  },
  mounted() {
    if (localStorage.getItem("items")) {
      this.items = JSON.parse(localStorage.getItem("items"));
    }
  },
  methods: {
    handleModalActive(state) {
      this.isAddModalActive = state;
    },

    searchItems(items) {
      this.items = items;
    },

    onAdditem(item) {
      // get the highest number id to iterate on it
      const highestId = Math.max.apply(Math, this.items.map(item => item.id));

      const { title, imageUrl, price, persons, doors, litres, description } = item;

      this.items.push({
        id: highestId + 1,
        title,
        imageUrl,
        price,
        persons,
        doors,
        litres,
        description,
      });

      this.saveLocalStorageitems();
      this.handleModalActive(false);
    },

    onClose() {
      this.handleModalActive(false);
    },

    deleteitem(item) {
       const index = this.items.indexOf(item);
        this.items.splice(index, 1);

        this.saveLocalStorageitems();
    },

    saveLocalStorageitems() {
      localStorage.setItem("items", JSON.stringify(this.items));
      this.items = JSON.parse(localStorage.getItem("items"));
    }
  }
}
</script>
