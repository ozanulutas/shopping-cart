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
			
			<b-navbar-nav>
				<b-nav-item v-b-modal.shopping-cart><i class="fas fa-shopping-cart"></i></b-nav-item>
				<b-nav-item v-b-modal.shopping-cart>{{shoppingCartItemsCount}}</b-nav-item>
			</b-navbar-nav>

			<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
			

			<b-collapse id="nav-collapse" is-nav>
				<!-- Right aligned nav items -->
				<b-navbar-nav class="ml-auto">
					<b-nav-form>
						<b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
						<b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
					</b-nav-form>
					<!-- <b-nav-item-dropdown text="Lang" right>
						<b-dropdown-item href="#">EN</b-dropdown-item>
						<b-dropdown-item href="#">ES</b-dropdown-item>
						<b-dropdown-item href="#">RU</b-dropdown-item>
						<b-dropdown-item href="#">FA</b-dropdown-item>
					</b-nav-item-dropdown>

					<b-nav-item-dropdown right>
						<template #button-content>
							<em>User</em>
						</template>
						<b-dropdown-item href="#">Profile</b-dropdown-item>
						<b-dropdown-item href="#">Sign Out</b-dropdown-item>
					</b-nav-item-dropdown> -->
				</b-navbar-nav>
			</b-collapse>
			
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