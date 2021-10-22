<template>
  <b-row
    align-h="center"
  >
    <b-col
      v-for="product in products" 
      :key="product.id"
      lg="6"
      md="12"
      class="d-flex justify-content-center"
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
      products, // ayakkabılar
    }
  },
  methods: {
    addToCart(product) { // Ürünün eklenmesi için App componentine emitler
      this.$emit("add-to-cart", product);
    }
  }
};
</script>

<style>
</style>