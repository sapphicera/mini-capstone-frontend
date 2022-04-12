<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newProductParams: {},
      // newImage: {},
      errors: [],
    };
  },
  created: function () { },
  methods: {
    createProduct: function () {
      axios.post("http://localhost:3000/products.json", this.newProductParams).then((response) => {
        console.log(response.data);
        // this is where the create img stuff would go i think... need to get imgs working
        this.$router.push("/products");
        this.newProductParams = {};
      }).catch((error) => {
        this.errors = error.response.data.errors;
      });
    },
    // createImage: function () {

    // }
  },
};
</script>

<template>
  <div class="products-new">
    <form v-on:submit.prevent="createProduct()">
      <h1>Edit Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newProductParams.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model="newProductParams.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="newProductParams.description" />
      </div>
      <div>
        <label>Stock:</label>
        <input type="text" v-model="newProductParams.stock" />
      </div>
      <div>
        <label>Supplier ID:</label>
        <input type="text" v-model="newProductParams.supplier_id" />
      </div>

      <!-- <div>
        <label>Image 1:</label>
        <input type="text" v-model="newImage.url" />
      </div> -->

      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style>
</style>