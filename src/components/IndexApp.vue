<template>
	<NavbarSite @changeMenu="changeMenu" />
	<div class="container">
		<div v-show="activeMenu == 'token'">
			<RequestToken @sendToken="catchToken" />
		</div>
		<div v-show="activeMenu == 'subscription'">
			<CreateSubscription :token="token" />
		</div>
		<div v-show="activeMenu == 'tokenPayment'">
			<RequestTokenPayment />
		</div>
	</div>
	<br />
	<div
		class="container align-items-center mt-5 d-flex p-2 justify-content-center"
	>
		<span class="d-flex justify-content-center"
			>Test de Sergio Naranjo para Kushki Colombia</span
		>
	</div>
</template>

<script>
import NavbarSite from "./NavbarSite.vue";
import RequestToken from "./RequestToken.vue";
import CreateSubscription from "./CreateSubscription.vue";
import RequestTokenPayment from "./RequestTokenPayment.vue";

export default {
	name: "IndexApp",
	components: {
		RequestToken,
		NavbarSite,
		CreateSubscription,
		RequestTokenPayment,
	},
	props: {
		msg: String,
	},
	data() {
		return {
			activeMenu: "token",
			token:"",
		};
	},
	methods: {
		catchToken(token) {
			this.token = token
		},
		changeMenu(menu) {
			this.activeMenu = menu;
		},
	},
};
</script>
