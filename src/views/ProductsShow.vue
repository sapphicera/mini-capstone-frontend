<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: [],
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
</template>

<style>
img {
  height: 200px;
  width: 200px;
}
</style>
