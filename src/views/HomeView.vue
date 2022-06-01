<script>
export default {
  data: function () {
    return {
      message: "hello and welcome to! ",
      samp: "sample",
      items: [{ message: "Foo" }, { message: "Bar" }, { message: "hello there" }],
      products: [
        { id: 1, name: "Product 1", price: 10 },
        { id: 2, name: "Product 2", price: 230 },
      ],
    };
  },
  created: function () {},
  methods: {
    helloWorld: function () {
      console.log("hello");
    },
    wordPlay: function () {
      console.log(this.message + this.samp);
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h3>{{ samp }}</h3>
    <p>helloWorld</p>
    <button v-on:click="helloWorld">hi</button>
    <button v-on:click="wordPlay">words</button>
    <li v-for="item in items" :key="item">
      {{ item.message }}
    </li>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>Name: {{ product.name }}</h2>
      <p>Price: {{ product.price }}</p>
    </div>
  </div>
</template>

<style></style>
