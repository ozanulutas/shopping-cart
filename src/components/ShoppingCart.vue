<template>
  <b-modal 
    id="shopping-cart" 
    :title="`Shopping Cart (${itemsCount})`"
    size="md"
    ok-only
    ok-title-html="<i class='fas fa-money-bill-wave'></i> SHUT UP AND TAKE MY MONEY"
    ok-variant="outline-primary"
    :hide-footer="itemsCount < 1"
    footer-border-variant="light"
  >
    <div v-if="itemsCount > 0">
      <p><b>Total Amount:</b> ${{ totalPrice }}</p>
      <CartItem 
        v-for="cartItem in shoppingCart"
        :key="cartItem.id"
        :product="cartItem"
        class="mb-2"
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
		product: {  // ProductCard componentinden sepete eklenen ürün
			type: Object,
			required: true,
		}
	},
	data() {
		return {
      shoppingCart: [], // Sepet
		}
	},
  computed: {
    // Sepetteki toplam ürün
    itemsCount() {
      let total = 0;
      this.shoppingCart.forEach(item => {
        item.sizes.forEach(size => total += size.quantity);
      });
      return total;
    },
    // Sepetin toplam tutarı
    totalPrice() {
      let total = 0;
      this.shoppingCart.forEach(item => {
        item.sizes.forEach(size => total += size.quantity * size.price);
      });
      return total;
    }
  },
	watch: {
    // product prop'undaki değişimi izler ve addToCart metodunu çağırır
		product: "addToCart",

    // Toplam ürün adedini izler App componentine emitler
    itemsCount: function(val) {
      this.$emit("items-count-change", val);
    }
	},
	methods: {
		// Ürün ekler
    addToCart() {
			// Shopping cart'ta olan aynı id'li ürün
      const sameProduct = this.shoppingCart.find(cartItem => cartItem.id === this.product.id);
			const [{size, quantity}] = this.product.sizes;

      if(sameProduct) { // Ürün varsa
				const sameSize = sameProduct.sizes.find(item => item.size === size);
				if(sameSize) { // ve aynı numaraysa numaranın miktarını artır
          this.increaseItem(sameSize, quantity);
				} else { // aynı numara değilse ürüne yeni numara ekle
					sameProduct.sizes.push(...this.product.sizes);
				}
      } else { // Ürün yoksa ekle
        this.shoppingCart.unshift(this.product);
      }

      this.makeToast();
    },
    // ürün modelini sepetten kaldırır
    removeFromCart(productId) {
      this.shoppingCart = this.shoppingCart.filter(cartItem => cartItem.id !== productId);
    },
    // ürün adedini artırır
    increaseItem(item, quantity) {
      item.quantity += quantity;
    },
    // ürün adedini 1 azaltır
    decreaseItem(item) {
      item.quantity--;
    },
    // ürün numarasını sepetten siler
    removeItem(product, sizeIndex) {
      product.sizes.splice(sizeIndex, 1);
    },

    // toast uyarı çıkarır
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
