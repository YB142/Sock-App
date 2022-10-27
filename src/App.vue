<template>
 <div id="app">
        <div class="cart">
            <p>Cart({{ cart.length }})</p>
        </div>
        <product :premium="premium" @add-to-cart="updateCart"></product>
    </div>
</template>

<script>
import Product from "./components/product.vue";
import "./style.css";

export default {
  name: 'App',
  components: {
    Product
  },
  data() {
    return ({
        premium: true,
        cart: [],
        errors: []
    })
  },
    methods: {
        updateCart(id) {
            this.cart.push(id)
        }
    },
}
</script>


<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>


