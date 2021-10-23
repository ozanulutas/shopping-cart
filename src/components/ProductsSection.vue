<template>
  <b-row
    align-h="center"
  >
    <b-col
      v-for="product in (filteredProducts.length > 0 ? filteredProducts : products)" 
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
  props: {
    colorFilters: {
      type: Array,
      required: false,
      default: () => [],
    }
  },
  data() {
    return {
      products, // ayakkabılar
      filteredProducts: [],
    }
  },
  watch: {
    colorFilters: function(filters) {

      console.log("filters", filters);

      // this.filteredProducts = this.products.filter(product => {
      //   return filters.includes(product.color);
      // });
      this.filteredProducts = [];
      let lastFilter = filters[filters.length - 1];

      this.products.forEach(product => {
        filters.forEach(filter => {
          for (const key in filter) {
            if(filter[key] === product[key]) {
              this.filteredProducts.push(product);
              let lastKey = key;
              let lastProduct = product;
            }
          }
        });
      });

      console.log(this.filteredProducts);
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