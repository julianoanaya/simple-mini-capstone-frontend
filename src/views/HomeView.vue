<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vues",
      samp: "sample",
      items: [{ message: "Foo" }, { message: "Bar" }, { message: "hello there" }],
      products: [],
      newProductParams: {},
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
    createProduct: function () {
      console.log("Creating product...");

      var params = this.newProductParams;

      axios
        .post("http://localhost:3000/products.json", params)
        .then((response) => {
          console.log("Created Product", response.data);
          this.products.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showProduct: function (product) {
      console.log("info is shown", product);
      document.querySelector("#product-details").showModal();
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>New Product</h2>
    <div>
      Name:
      <input type="text" v-model="newProductParams.name" />
    </div>
    <div>
      Price:
      <input type="text" v-model="newProductParams.price" />
    </div>
    <div>
      description:
      <input type="text" v-model="newProductParams.description" />
    </div>
    <div>
      image_url:
      <input type="text" v-model="newProductParams.image_url" />
    </div>
    <button v-on:click="createProduct()">Create Product</button>
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
      <button v-on:click="showProduct">Show info...</button>
    </div>

    <dialog id="product-details">
      <form method="dialog">
        <h2>Product info:</h2>
        <p>Name: ...</p>
        <p>Price: ...</p>
        <p>Description: ...</p>
        <p>Price: ...</p>
        <button>Close window</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>
