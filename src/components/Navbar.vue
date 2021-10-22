<template>
	<b-navbar
		toggleable="md"
		type="dark"
		variant="dark"
		sticky
		class="mb-5"
	>
		<b-container>
			<b-navbar-brand>Nike</b-navbar-brand>
			
			<b-navbar-nav class="ml-auto">
				<b-nav-item v-b-modal.shopping-cart>
					<i class="fas fa-shopping-cart"></i>
					<b-badge pill variant="dark">{{shoppingCartItemsCount}}</b-badge>
				</b-nav-item>
			</b-navbar-nav>

			<!-- <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

			<b-collapse id="nav-collapse" is-nav>
				<b-navbar-nav class="ml-auto">
					<b-nav-form>
						<b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
						<b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
					</b-nav-form>
					
				</b-navbar-nav>
			</b-collapse> -->
			
		</b-container>
		
  </b-navbar>
</template>

<script>

export default {
	name: "Navbar",
	props: {
    shoppingCartItemsCount: {
      type: Number,
      required: true,
    }
  },
	components: {
	},
};
</script>

<style>
</style>