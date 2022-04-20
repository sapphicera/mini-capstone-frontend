<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editProductParams: {},
      suppliers: [],
      errors: [],
    };
  },
  created: function () {
    axios.get(`/products/${this.$route.params.id}.json`).then((response) => {
      this.editProductParams = response.data;
      // this.suppliers = response.data.all_suppliers;
    })
    axios.get("/suppliers.json").then((response) => {
      this.suppliers = response.data;
    })
  },
  methods: {
    editProduct: function () {
      console.log(this.editProductParams);
      console.log("pending...")
      axios.patch(`/products/${this.$route.params.id}.json`, this.editProductParams).then((response) => {
        console.log(response.data);
        this.$router.push(`/products/${this.$route.params.id}`);
      }).catch((error) => {
        this.errors = error.response.data.errors;
      });
    }
  },
};
</script>

<template>
  <div class="products-edit">
    <h1>Edit Product</h1>

    <ul>
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="editProduct()">
      <div>
        <label>Name:</label>
        <input type="text" v-model="editProductParams.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model="editProductParams.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="editProductParams.description" />
      </div>
      <div>
        <label>Stock:</label>
        <input type="text" v-model="editProductParams.stock" />
      </div>

      <div>
        <label>Supplier ID:</label>
        <input type="text" v-model="editProductParams.supplier_id" />
      </div>

      <!-- <label for="suppliers">Supplier:</label>

      <select name="suppliers" id="suppliers" v-model="editProductParams.supplier_id">
        <option v-for="supplier in suppliers" v-bind:key="supplier.id">{{ supplier.name }}</option>

      </select> -->

      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style>
</style>