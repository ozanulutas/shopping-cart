<template>
  <div id="app">
    <Navbar />
		<ShoppingCart 
      :product="product"
    />

    <b-container>
      <ProductsSection
        @add-to-cart="addToCart"
      />
    </b-container>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import ShoppingCart from "@/components/ShoppingCart.vue";
import ProductsSection from "@/components/ProductsSection.vue";

export default {
  name: "App",
  components: {
    Navbar,
		ShoppingCart,
    ProductsSection,
  },
  data() {
    return {
      product: {},
    }
  },
  methods: {
    addToCart(product) {
      // console.log(product);
      this.product = product;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
