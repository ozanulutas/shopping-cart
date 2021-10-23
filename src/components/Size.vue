<template>
  <div class="d-flex justify-content-between">
		<div>
			<b>Size:</b> {{ item.size }} x {{ item.quantity }} pairs 
		</div>
		<div>
			<b-button 
				size="sm" 
				variant="link" 
				class="p-0 mr-1"
				@click="$emit('decrease')"
			>
				<i class="fas fa-minus-circle"></i>
			</b-button> 
			<b-button 
				size="sm" 
				variant="link" 
				class="p-0 mr-3"
				@click="$emit('increase')"
			>
				<i class="fas fa-plus-circle"></i>
			</b-button>
			<b-button 
				size="sm" 
				variant="link" 
				class="p-0 text-danger"
				@click="$emit('remove-item')"
			>
				<i class="fas fa-trash-alt"></i>
			</b-button>
		</div>
  </div>
</template>

<script>

export default {
	name: "Size",
  props: {
    item: {	// Ürüne ait numara
      type: Object,
      required: true,
    }
  },
  watch: {
		// Sepette numaraya ait kaç adet ürün olduğunu izler.
		// Adet 0'a düştüğünde ürüne ait numaranın spetten silinmesi için ShoppingCart componentine emitler
    "item.quantity": function(val) {
      if(val < 1) {
        this.$emit('remove-item');
      }
    }
  }
}
</script>

<style>

</style>