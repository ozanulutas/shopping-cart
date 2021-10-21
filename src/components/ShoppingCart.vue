<template>
  <b-modal 
    id="shopping-cart" 
    title="Shopping Cart"
    size="md"
  >
    <div v-if="isCartEmpty">
    <CartItem 
      v-for="cartItem in shoppingCart"
      :key="cartItem.id"
      :product="cartItem"
      @increase="increaseItem"
      @decrease="decreaseItem"
      @remove-item="removeItem"
      @remove-product="removeFromCart"
    />
    </div>
    <p v-else>
      There are no products in your cart.
    </p>
	</b-modal>
</template>

<script>
import CartItem from "@/components/CartItem.vue";

export default {
  name: "ShoppingCart",
  components: {
    CartItem,
  },
  props: {
		product: {
			type: Object,
			required: true,
		}
	},
	data() {
		return {
      shoppingCart: [],
		}
	},
  computed: {
    isCartEmpty() {
      return this.shoppingCart.length;
    }
  },
	watch: {
		product: "addToCart"
	},
	methods: {
		// Ürün ekler
    addToCart() {
      // console.log("product from card", this.product);
			// Shopping cart'ta olan aynı id'li ürün
      const sameProduct = this.shoppingCart.find(cartItem => cartItem.id === this.product.id);
			const [{size, quantity}] = this.product.sizes;
      // console.log("size", size);
      // console.log("same product", sameProduct);

      if(sameProduct) { // Ürün varsa quantity'sini artır
				const sameSize = sameProduct.sizes.find(item => item.size === size);
				if(sameSize) {
					// sameSize.quantity += quantity;
          this.increaseItem(sameSize, quantity);
				} else {
					sameProduct.sizes.push(...this.product.sizes);
				}
      } else { // Ürün yoksa ekle
        this.shoppingCart.unshift(this.product);
      }

      // console.log("shopping cart", this.shoppingCart);
      // console.log("===================================");
    },
    removeFromCart(productId) {
      this.shoppingCart = this.shoppingCart.filter(cartItem => cartItem.id !== productId);
    },
    increaseItem(item, quantity) {
      item.quantity += quantity;
    },
    decreaseItem(item) {
      item.quantity--;
    },
    removeItem(product, sizeIndex) {
      product.sizes.splice(sizeIndex, 1);
    }
	}
}
</script>

<style>

</style>