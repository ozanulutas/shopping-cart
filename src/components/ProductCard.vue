<template>
  <b-card
    no-body 
    align="left" 
    class="product-card shadow" 
  >
    <b-row no-gutters>
      <b-col md="7">
        <b-card-body>
          <b-card-img
            :src="product.img"
            alt="Image"
            class="rounded-0"
          ></b-card-img>
        </b-card-body>
      </b-col>
      <b-col md="5">
        <b-card-body>
          <h6 class="product-card__subtitle">{{ product.category }}</h6>
          <b-card-title>{{ product.name }}</b-card-title>
          <h3 class="product-card__price">${{ price }}</h3>
          <b-card-text class="text-justify">
            {{ product.desc }}
          </b-card-text>
          <div class="d-flex">
            <i v-for="i in product.rating" :key="`f-${i}`" class="fas fa-star text-warning"></i>
            <i v-for="i in (5 - product.rating)" :key="`e-${i}`" class="fas fa-star"></i>
          </div>
        </b-card-body>
      </b-col>
    </b-row>
    <b-row no-gutters>
      <b-col md="7">
        <b-card-body>
          <!-- Size -->
          <h6 class="product-card__subtitle">CHOOSE SIZE</h6>
            <b-form-radio-group
              :options="product.sizes"
              v-model="size"
              class="product-card__sizes"
              buttons
              button-variant=" btn--product-card btn--size btn--pink"
            ></b-form-radio-group>
        </b-card-body>
        
      </b-col>
      <b-col md="5" align-self="end">
        <b-card-body class="d-flex gap-1q">
          <!-- Add -->
          <button
           block 
           class="btn btn--product-card btn--pink"
           @click="addToCart(product)"
          >
            ADD TO CART
          </button>

          <!-- Quantity -->
          <b-dropdown 
            size="md" 
            class="product-card__quantity"
            toggle-class="btn--pink" 
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
    product: {
      type: Object,
      required: true,
    }
    // id: {
    //   type: Number,
    //   required: true,
    // },
    // name: {
    //   type: String,
    //   required: true,
    // },
    // category: {
    //   type: String,
    //   required: true,
    // },
    // desc: {
    //   type: String,
    //   required: true,
    // },
    // img: {
    //   type: String,
    //   required: true,
    // },
    // rating: {
    //   type: Number,
    //   required: false,
    // },
    // price: {
    //   type: Number,
    //   required: true,
    // },
    // sizes: {
    //   type: Array,
    //   required: true,
    // },
  },
  data() {
    return {
      quantity: 1,
      size: 4,
      sizeMultiplier: 1.5,
    }
  },
  computed: {
    price() {
      return this.product.price + (this.sizeMultiplier * this.size);
    }
  },
  methods: {
    // Ürün miktarını belirler
    setQuantity(quantity) {
      this.quantity = quantity;
    },

    // Ürün ekler
    addToCart(product) {
      this.$emit("add-to-cart", {
        size: this.size,
        quantity: this.quantity,
        _price: this.price,
        ...product,
      });
      
      // const [sameProduct] = this.shoppingCart.filter(cartItem => cartItem.id === product.id);

      // if(sameProduct) { // Ürün varsa quantity'sini artır
      //   sameProduct.quantity += this.quantity;
      // } else { // Ürün yoksa ekle
      //   this.shoppingCart.unshift({
      //     size: this.size,
      //     quantity: this.quantity,
      //     _price: this.price,
      //     ...product,
      //   });
      // }

      this.setQuantity(1); // Ürün miktarını resetle
      // console.log(this.shoppingCart);
    }
  }
};
</script>
