<template>
  <div id="app">
    <Navbar 
      :shopping-cart-items-count="shoppingCartItemsCount"
    />
		<ShoppingCart 
      :product="product"
      @items-count-change="(val) => shoppingCartItemsCount = val"
    />

    <main class="custom-container">
      <ProductsSection
        @add-to-cart="addToCart"
      />
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
      product: {}, // Sepete eklenecek olan ürün
      shoppingCartItemsCount: 0, // Sepetteki toplam ütün adedi
    }
  },
  methods: {
    // ProductCard componentinden emitlenen ürün bilgisini yakalar
    addToCart(product) {
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
