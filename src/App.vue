<template>
  <div class="nav-bar"></div>
  <div class="product-display">
    <div class="cart"
    :style="{width:'5rem'}">Cart ( {{ cart.length }} )</div>
    <div class="product-container">

      <ProductDisplay
          :premium="premium"
          @add-to-cart="updateCart" />

    </div>
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay";


export default {
  name: 'App',
  components: {ProductDisplay},
  data() {
    return {
      cart: [],
      premium: true
    }
  },
  methods: {
    updateCart(id){
      this.cart.push(id)
    }

  },

}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
