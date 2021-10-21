<template>
  <div>
    <b>Size:</b> {{ item.size }} x {{ item.quantity }} pairs 
		<b-button 
			size="sm" 
			variant="link" 
			class="p-0"
			@click="$emit('decrease')"
		>
			<i class="fas fa-minus-square"></i>
		</b-button> 
		<b-button 
			size="sm" 
			variant="link" 
			class="p-0"
			@click="$emit('increase')"
		>
			<i class="fas fa-plus-square"></i>
		</b-button>
		<b-button 
			size="sm" 
			variant="link" 
			class="p-0"
			@click="$emit('remove-item')"
		>
			<i class="fas fa-trash-alt"></i>
		</b-button>
  </div>
</template>

<script>

export default {
	name: "Size",
  props: {
    item: {
      type: Object,
      required: true,
    }
  },
  watch: {
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