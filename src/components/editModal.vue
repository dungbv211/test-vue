<template>
  <div id="editModal" class="form-input">
    <h2>Edit Product</h2>
    <label for="editedName">Name:</label>
    <input type="text" id="editedName" v-model="editTask.name" />
    <label for="editedInStock">In Stock:</label>
    <input type="number" id="editedInStock" v-model="editTask.inStock" />
    <label for="editedPrice">Price:</label>
    <input type="number" id="editedPrice" v-model="editTask.price" />
    <label for="editedName">description:</label>
    <input type="text" id="editedDescription" v-model="editTask.description" />
    <div class="d-flex justify-content-between">
      <button @click="saveEdit" class="btn btn-info">Save</button>
      <button @click="cancelEdit" class="btn btn-danger">Cancel</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TestVueEditModal",

  data() {
    return {
      editingProduct: null,
      editTask: {},
    };
  },

  mounted() {},

  methods: {
    saveEdit() {
      if (this.editingProduct !== null) {
        const index = this.products.indexOf(this.editingProduct);
        this.products[index] = { ...this.editingProduct };
        this.updateTable();
        this.editingProduct = null;
      }
    },
    updateTable() {
      this.deleteProduct();
      this.products.push({
        editingName: this.name,
        editingInStock: this.inStock,
        editingPrice: this.price,
        editingDescription: this.description,
      });
    },
    cancelEdit() {
      this.editingProduct = null;
    },
  },
};
</script>

<style lang="scss" scoped></style>
