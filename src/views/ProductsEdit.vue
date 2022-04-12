<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editProductParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`http://localhost:3000/products/${this.$route.params.id}.json`).then((response) => {
      console.log(response.data);
      this.editProductParams = response.data;
    })
  },
  methods: {
    editProduct: function () {
      axios.patch(`http://localhost:3000/products/${this.$route.params.id}.json`, this.editProductParams).then((response) => {
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
    <form v-on:submit.prevent="editProduct()">
      <h1>Edit Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
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
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style>
</style>