<template>
  <div id="app">
    <header-modal
      @handle-modal-active="handleModalActive"
    ></header-modal>
    <search-modal></search-modal>
    <table-modal
      :items="items"
      @delete-item="deleteitem"
    >
    </table-modal>

    <add-modal
      v-if="isAddModalActive"
      @add-item="onAdditem"
      @close-item="onClose"
    ></add-modal>
  </div>
</template>

<script>
import TableModal from "@/components/TableModal.vue";
import SearchModal from "@/components/SearchModal.vue";
import HeaderModal from "@/components/HeaderModal.vue";
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
    } else {
      this.items = this.initialitems;
    }
  },
  methods: {
    handleModalActive(state) {
      this.isAddModalActive = state;
    },

    onAdditem(item) {
      // get the highest number id to iterate on it
      const highestId = Math.max.apply(Math, this.items.map(item => item.id));

      this.items.push({
        id: highestId + 1,
        title: item.title,
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
