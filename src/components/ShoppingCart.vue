<template>
  <b-modal 
    id="shopping-cart" 
    title="Shopping Cart"
    size="md"
  >
    <div v-if="itemsCount > 0">
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
    itemsCount() {
      let total = 0;
      this.shoppingCart.forEach(item => {
        item.sizes.forEach(size => total += size.quantity);
      });
      return total;
    }
  },
	watch: {
		product: "addToCart",
    itemsCount: function(val) {
      console.log(val);
      this.$emit("items-count-change", val);
    }
	},
	methods: {
		// Ürün ekler
    addToCart() {
			// Shopping cart'ta olan aynı id'li ürün
      const sameProduct = this.shoppingCart.find(cartItem => cartItem.id === this.product.id);
			const [{size, quantity}] = this.product.sizes;

      if(sameProduct) { // Ürün varsa quantity'sini artır
				const sameSize = sameProduct.sizes.find(item => item.size === size);
				if(sameSize) {
          this.increaseItem(sameSize, quantity);
				} else {
					sameProduct.sizes.push(...this.product.sizes);
				}
      } else { // Ürün yoksa ekle
        this.shoppingCart.unshift(this.product);
      }

      this.makeToast();
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
    },

    makeToast() {
      this.$bvToast.toast(`${this.product.name} has been added to your cart.`, {
        title: this.product.name,
        toaster: "b-toaster-bottom-center",
        solid: true,
        appendToast: false
      });
    }
	}
}
</script>

<style>

</style>