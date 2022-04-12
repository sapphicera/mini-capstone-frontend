<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: {},
    };
  },
  created: function () {
    this.showProduct();
  },
  methods: {
    showProduct: function () {
      axios.get(`http://localhost:3000/products/${this.$route.params.id}.json`).then((response) => {
        console.log(response.data);
        this.product = response.data;
      })
    },
    deleteProduct: function () {
      console.log("deleting...");
      axios.delete(`http://localhost:3000/products/${this.$route.params.id}.json`).then((response) => {
        console.log(response.data);
        this.$router.push("/products");
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ product.name }}</h1>
  </div>
  <br />
  {{ product.description }}
  <br />
  <div v-for="image in product.images" v-bind:key="image.url">
    <img v-bind:src="image.url" />
  </div>
  <br />
  <router-link v-bind:to="`/products/${product.id}/edit`" class="btn btn-primary">Update</router-link> |
  <button @click="deleteProduct()">Delete Product</button> |
  <router-link v-bind:to="`/products`" class="btn btn-primary">Back to Index</router-link>
</template>

<style>
img {
  height: 200px;
  width: 200px;
}
</style>
