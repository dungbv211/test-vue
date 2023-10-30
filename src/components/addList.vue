<template>
  <div class="container-main p-5">
    <div id="app">
      <form @submit.prevent="submitForm" class="form-input">
        <h2>Add List</h2>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" required />
        <label for="inStock">In Stock:</label>
        <input type="number" id="inStock" v-model="inStock" required />
        <label for="price">Price:</label>
        <input type="number" id="price" v-model="price" required />
        <label for="description">description</label>
        <input type="text" id="description" v-model="description" />
        <button type="submit" @click="submitForm()" class="btn btn-info">Submit</button>
      </form>

      <table class="table">
        <thead>
          <tr>
            <th>Name</th>
            <th>In Stock</th>
            <th>Price</th>
            <th>Description</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product, index) in products" :key="index">
            <td>
              {{ product.name }}
            </td>
            <td>
              <button
                :style="{
                  backgroundColor: product.inStock < 50 ? 'red' : 'green',
                  borderRadius: '5px',
                  color: 'white',
                }"
              >
                {{ product.inStock }}
              </button>
            </td>
            <td>{{ product.price }}</td>
            <td>{{ product.description }}</td>
            <td>
              <button @click="deleteProduct(index)" class="btn btn-danger">
                Del
              </button>
              <button @click="editProduct(product)" class="btn btn-primary">
                Edit
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div id="editModal" v-if="editingProduct !== null" class="form-input">
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
  </div>
</template>

<script>
export default {
  name: "TestVue",

  data() {
    return {
      name: "",
      inStock: "",
      price: "",
      description: "",
      products: [],
      editingProduct: null,
      editTask:{}
    };
  },

  mounted() {},
  computed: {
    isFormValid() {
      return (
        this.name !== "" &&
        this.inStock !== "" &&
        this.price !== "" &&
        this.description !== ""
      );
    },
  },

  methods: {
    submitForm() {
      if (this.isFormValid) {
        this.products.unshift({
          name: this.name,
          inStock: this.inStock,
          price: this.price,
          description: this.description,
        });
        this.name = "";
        this.inStock = "";
        this.price = "";
        this.description = "";
      }
    },
    deleteProduct(index) {
      this.products.splice(index, 1);
    },
    editProduct(product) {
      this.editingProduct = { ...this.products[product] };
      this.editTask = product
    },
    saveEdit() {
      if (this.editingProduct !== null) {
        const index = this.products.indexOf(this.editingProduct);
        this.products[index] = { ...this.editingProduct };
        this.updateTable();
        this.editingProduct = null;
      }
    },
    cancelEdit() {
      this.editingProduct = null;
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
  },
};
</script>

<style scoped>
.container-main {
  margin: 0 auto;
  max-width: 1000px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
#app {
  display: flex;
  flex-direction: row;
}
.form-input {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  text-align: left;
  width: 300px;
  gap: 10px;
}
.form-input input {
  height: 30px;
  border-radius: 5px;
}
.form-input label {
  font-size: medium;
  font-weight: 700;
}
</style>
