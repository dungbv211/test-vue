<template>
  <div class="container-main p-5">
    <div class="container-input">
      <div>
        <label>Name:</label>
        <input
          v-model="formData.name.value"
          type="text"
          :state="nameError"
          placeholder="Enter your name"
          trim
          @blur="hadlerFormclickName"
        />
        <p v-show="formData.name.isDirty && !nameError">Enter your name</p>
      </div>
      <div>
        <label>In Stock:</label>
        <input
          v-model="formData.stock.value"
          type="text"
          :state="stockError"
          placeholder="Enter stock"
          trim
          @blur="hadlerFormclickStock"
        />
        <p v-show="formData.stock.isDirty && !stockError">Enter Stock</p>
      </div>
      <div>
        <label>Price:</label>
        <input
          v-model="formData.price.value"
          type="text"
          :state="priceError"
          placeholder="Enter price"
          @blur="hadlerFormclickPrice"
        />
        <p v-show="formData.price.isDirty && !priceError">Enter price</p>
      </div>
      <div>
        <label>description:</label>
        <input
          v-model="formData.description.value"
          type="text"
          :state="descriptionError"
          placeholder="Enter description"
          trim
          @blur="hadlerFormclickDescription"
        />
        <p v-show="formData.description.isDirty && !descriptionError">
          Enter description
        </p>
      </div>
      <div class="d-flex">
        <button
          class="add-item"
          type="submit"
          :disabled="isFormValid"
          @click="handleSubmit()"
        >
          Submit
        </button>
      </div>
      <table>
        <tr>
          <td>name</td>
          <td>In Stock</td>
          <td>price</td>
          <td>description</td>
          <td>action</td>
        </tr>
        <tr v-for="(item, index) in formData" :key="index">
          <td>{{ item.name }}</td>
          <td>{{ item.stock }}</td>
          <td>{{ item.price }}</td>
          <td>{{ item.description }}</td>
          <td>
            <button @click="handlerDelete(item)">delete</button>
            <button @click="handleEdit()">edit</button>
          </td>
        </tr>
      </table>
    </div>
    <table></table>
  </div>
</template>

<script>
export default {
  name: "TestVue",

  data() {
    return {
      formData: {
        name: {
          value: "",
          error: true,
          isDirty: false,
        },
        stock: {
          value: "",
          error: true,
          isDirty: false,
        },
        price: {
          value: "",
          error: true,
          isDirty: false,
        },
        description: {
          value: "",
          error: true,
          isDirty: false,
        },
      },
    };
  },

  mounted() {},
  computed: {
    nameError() {
      if (!this.formData.name.isDirty) {
        return null;
      }
      return this.formData.name.value.length > 5;
    },
    stockError() {
      if (!this.formData.stock.isDirty) {
        return null;
      }
      return this.formData.stock.value.length > 5;
    },
    priceError() {
      if (!this.formData.price.isDirty) {
        return null;
      }
      return this.formData.price.value.length > 5;
    },
    descriptionError() {
      if (!this.formData.description.isDirty) {
        return null;
      }
      return this.formData.description.value.length > 5;
    },
    isFormValid() {
      return (
        this.formData.name.value.length > 5 &&
        this.formData.stock.value.length > 5 &&
        this.formData.price.value.length > 5 &&
        this.formData.description.value.length > 5
      );
    },
  },

  methods: {
    hadlerFormclickName() {
      this.formData.name.isDirty = true;
    },
    hadlerFormclickStock() {
      this.formData.stock.isDirty = true;
    },
    hadlerFormclickPrice() {
      this.formData.price.isDirty = true;
    },
    hadlerFormclickDescription() {
      this.formData.description.isDirty = true;
    },
    handleSubmit() {
        if (!this.formData.name.value || !this.formData.stock.value || !this.formData.price.value || !this.formData.description.value) {
        console.log("failed");
      } else {
        this.formData.push({
          name: this.formData.name.value,
          stock: this.formData.stock.value,
          price: this.formData.price.value,
          description: this.formData.description.value,
        });
      }
    },
    handlerDelete() {
      const index = this.formData.findIndex(
        (item) => item.id === this.formData.id
      );
      if (index >= 0) {
        this.formData.splice(index, 1);
      }
    },
    handleEdit(){

    }
  },
};
</script>

<style scoped>
.container-main {
  margin: 0 auto;
  max-width: 800px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.container-input {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
