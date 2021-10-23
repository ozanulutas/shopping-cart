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
				<b-nav-item v-b-toggle.sidebar-1>
					Toggle Sidebar
				</b-nav-item>
				<b-nav-item v-b-modal.shopping-cart>
					<i class="fas fa-shopping-cart"></i>
					<b-badge pill variant="dark">{{shoppingCartItemsCount}}</b-badge>
				</b-nav-item>
			</b-navbar-nav>
			
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