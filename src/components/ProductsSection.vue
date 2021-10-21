<template>
  <section>
		<ProductCard 
      v-for="product in products" 
      :key="product.id"
      :product="product"
      @add-to-cart="addToCart"
    />
	</section>
</template>

<script>
import ProductCard from "@/components/ProductCard.vue";
import products from "@/data/products.js"

export default {
  name: "ProductsSection",
  components: {
    ProductCard,
  },
  data() {
    return {
      products,
    }
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    }
  }
};
</script>

<style>
</style>