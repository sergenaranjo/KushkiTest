<template>
	<nav class="navbar navbar-expand-lg border-bottom bg-light bg-gradient">
		<div class="container-fluid">
			<a class="navbar-brand text-dark" href="#">Kushki Test</a>
			<button
				class="navbar-toggler"
				type="button"
				data-bs-toggle="collapse"
				data-bs-target="#navbarSupportedContent"
				aria-controls="navbarSupportedContent"
				aria-expanded="false"
				aria-label="Toggle navigation"
			>
				<span class="navbar-toggler-icon"></span>
			</button>
			<div class="collapse navbar-collapse" id="navbarSupportedContent">
				<ul class="navbar-nav me-auto mb-2 mb-lg-0">
					<li class="nav-item">
						<a
							class="nav-link"
							:class="{
								'link-primary': activeMenu == 'token',
								'link-dark': activeMenu != 'token',
							}"
							aria-current="page"
							@click="changeMenu('token')"
							href="#"
							>Token Suscripción</a
						>
					</li>
					<li class="nav-item">
						<a
							class="nav-link"
							:class="{
								'link-primary': activeMenu == 'subscription',
								'link-dark': activeMenu != 'subscription',
							}"
							@click="changeMenu('subscription')"
							aria-current="page"
							href="#"
							>Suscripción</a
						>
					</li>
					<li class="nav-item">
						<a
							class="nav-link"
							:class="{
								'link-primary': activeMenu == 'tokenPayment',
								'link-dark': activeMenu != 'tokenPayment',
							}"
							@click="changeMenu('tokenPayment')"
							aria-current="page"
							href="#"
							>Token Pago</a
						>
					</li>
				</ul>
			</div>
		</div>
	</nav>
</template>

<script>
export default {
	data() {
		return {
			activeMenu: "token",
		};
	},
	name: "NavbarSite",
	methods: {
		changeMenu(menu) {
			this.$emit("changeMenu", menu);
			this.activeMenu = menu;
		},
	},
};
</script>
