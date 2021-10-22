<template>
  <b-row
    align-h="center"
  >
    <b-col
      lg="6"
      md="12"
      v-for="product in products" 
      :key="product.id"
    >
      <ProductCard 
        :product="product"
        @add-to-cart="addToCart"
      />
    </b-col>
	</b-row>
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