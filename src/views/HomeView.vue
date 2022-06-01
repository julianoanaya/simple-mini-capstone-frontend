<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vues",
      samp: "sample",
      items: [{ message: "Foo" }, { message: "Bar" }, { message: "hello there" }],
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    helloWorld: function () {
      console.log("hello");
    },
    wordPlay: function () {
      console.log(this.message + this.samp);
    },
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        this.products = response.data;
        console.log("All products", response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- <h3>{{ samp }}</h3>
    <p>helloWorld</p>
    <button v-on:click="helloWorld">hi</button>
    <button v-on:click="wordPlay">words</button>
    <li v-for="item in items" :key="item">
      {{ item.message }}
    </li> -->
    <div v-for="product in products" v-bind:key="product.id">
      <h1>Name: {{ product.name }}</h1>
      <img v-bind:src="product.image_url" v-bind:alt="product.title" />
      <p>Price: {{ product.price }}</p>
    </div>
  </div>
</template>

<style></style>
