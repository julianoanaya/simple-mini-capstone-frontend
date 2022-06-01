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
      editProductParams: {},
      currentProduct: {},
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
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#product-details").showModal();
    },
    updateProduct: function () {
      console.log("updating product...", this.editProductParams);
      axios
        .patch("http://localhost:3000/products/" + this.editProductParams.id + ".json", this.editProductParams)
        .then((response) => {
          console.log("Success", response.date);
        });
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
      <button v-on:click="showProduct(product)">Show info...</button>
    </div>

    <dialog id="product-details">
      <form method="dialog">
        <h2>Product info:</h2>
        <p>Name: {{ currentProduct.name }}</p>
        <p>Price: {{ currentProduct.price }}</p>
        <p>Description: {{ currentProduct.description }}</p>
        <p>Tax: {{ currentProduct.tax }}</p>
        <p>Total: {{ currentProduct.total }}</p>
        <h1>Edit Product:</h1>
        <p>
          Name:
          <input type="text" v-model="editProductParams.name" />
        </p>
        <p>
          Price:
          <input type="text" v-model="editProductParams.price" />
        </p>
        <p>
          Description:
          <input type="text" v-model="editProductParams.description" />
        </p>
        <p>
          Image_url:
          <input type="text" v-model="editProductParams.image_url" />
        </p>
        <p><button v-on:click="updateProduct()">Update Product</button></p>
        <button>Close Window</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>
