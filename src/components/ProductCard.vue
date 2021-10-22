<template>
  <b-card
    no-body
    align="left"
    class="product-card shadow m-2"
  >
    <b-row no-gutters>
      <b-col md="7" align-self="center">
        <b-card-body>
          <!-- Img -->
          <b-card-img
            :src="product.img"
            alt="Image"
            class="rounded-0"
          ></b-card-img>
        </b-card-body>
      </b-col>
      <b-col md="5">
        <b-card-body>
          <!-- Category -->
          <h6 class="product-card__subtitle" :class="`text-${product.color}`">{{ product.category }}</h6>
          <!-- Name -->
          <b-card-title>{{ product.name }}</b-card-title>
          <!-- Price -->
          <h3 class="product-card__price" :class="`text-${product.color}`">${{ price }}</h3>
          <!-- Desc -->
          <b-card-text class="text-justify">
            {{ product.desc }}
          </b-card-text>
          <!-- Rating -->
          <div class="d-flex">
            <i v-for="i in product.rating" :key="`f-${i}`" class="fas fa-star" :class="`text-${product.color}`"></i>
            <i v-for="i in (5 - product.rating)" :key="`e-${i}`" class="fas fa-star text-muted"></i>
          </div>
        </b-card-body>
      </b-col>
    </b-row>
    <b-row no-gutters>
      <b-col md="7">
        <b-card-body>
          <!-- Size -->
          <h6 class="product-card__subtitle" :class="`text-${product.color}`">CHOOSE SIZE</h6>
            <b-form-radio-group
              :options="product.sizes"
              v-model="size"
              class="product-card__sizes"
              buttons
              :button-variant="` btn--product-card btn--size btn--${product.color}`"
            ></b-form-radio-group>
        </b-card-body>

      </b-col>
      <b-col md="5" align-self="end">
        <b-card-body class="d-flex gap-1q">
          <!-- Add To Cart -->
          <button
           block
           class="btn btn--product-card btn--pink"
           :class="`btn--${product.color}`"
           @click="addToCart(product)"
          >
            ADD TO CART
          </button>

          <!-- Quantity -->
          <b-dropdown
            size="md"
            class="product-card__quantity"
            :toggle-class="`btn--${product.color}`"
            no-caret
          >
            <template #button-content>
              {{ quantity }}
            </template>
            <b-dropdown-item
              v-for="i in 10" :key="i"
              @click="setQuantity(i)"
            >
              {{i}} Pairs
            </b-dropdown-item>
          </b-dropdown>
        </b-card-body>
      </b-col>
    </b-row>
  </b-card>
</template>

<script>

export default {
  name: "ProductCard",
  props: {
    product: { // ProductSection componentinden gelen prop
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      quantity: 1, // Ürün adedi
      size: 4,  // Ürün numarası
      sizeMultiplier: 1.5,  // Ayakkabı numarası çarpanı
    }
  },
  computed: {
    // Ayakkabı numarasına göre fiyatı hesaplar
    price() {
      return this.product.price + (this.sizeMultiplier * this.size);
    }
  },
  // watch: {
  //   'product.sizes': function() {
  //     console.log("changed");
  //   }
  // },
  methods: {
    // Ürün miktarını belirler
    setQuantity(quantity) {
      this.quantity = quantity;
    },

    // Ürünün eklenmesi için App componentine emitler
    addToCart(product) {
      this.$emit("add-to-cart", {
        id: product.id,
        name: product.name,
        category: product.category,
        color: product.color,
        img: product.img,
        sizes: [
          {
            size: this.size,
            price: this.price,
            quantity: this.quantity,
          }
        ]
      });

      this.setQuantity(1); // Ürün miktarını resetle
    }
  }
};
</script>
