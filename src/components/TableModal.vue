<template>
  <div>
    <section>
      <div>
        <table>
          <template>
            <tr
              v-for="item in items"
              :key="item.id"
            >
              <td label="item" field="item" sortable>
                {{ item.title }}
              </td>

              <td label="Delete">
                <button
                  @click="$emit('delete-item', item.row)"
                >Delete</button>
              </td>
            </tr>
          </template>
        </table>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: "TableModal",
  props: {
    items: {
      type: Array,
      required: true
    }
  },
};
</script>

<style lang="scss" scoped></style>