<template>
  <div id="app">
    <Navbar 
      :shopping-cart-items-count="shoppingCartItemsCount"
    />
		<ShoppingCart 
      :product="product"
      @items-count-change="(val) => shoppingCartItemsCount = val"
    />

    <main class="main">
      <!-- <b-container> -->

      <ProductsSection
        @add-to-cart="addToCart"
      />
      <!-- </b-container> -->

    </main>
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
      shoppingCartItemsCount: 0,
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

.main {
  max-width: 1300px;
  width: 100%;
  margin: auto;
  padding: 1rem;
}
</style>
