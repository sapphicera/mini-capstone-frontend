<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        console.log(response.data);
        this.products = response.data;
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>ALL PRODUCTS</h1>
  </div>
  <div v-for="product in products" v-bind:key="product.id">
    {{ product.id }}. {{ product.name }}
    <br />
    {{ product.description }}
    <br />
    <div v-for="image in product.images" v-bind:key="image.url">
      <img v-bind:src="image.url" />
    </div>

    <!-- {{ product.images.url }} <br /> -->
    <br />
  </div>
</template>

<style>
img {
  height: 200px;
  width: 200px;
}
</style>
