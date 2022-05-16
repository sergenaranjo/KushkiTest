<template>
	<h1 class="my-5">Creación de Suscripción</h1>
	<div class="card bg-light">
		<div class="card-body">
			<div class="mb-3 row">
				<label for="inputToken" class="col-sm-2 col-form-label">Token</label>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputToken"
						v-model="inputToken"
						disabled
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputPlanName" class="col-sm-2 col-form-label"
					>Nombre del Plan</label
				>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputPlanName"
						v-model="inputPlanName"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputDocumentType" class="col-sm-2 col-form-label"
					>Tipo de Documento</label
				>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputDocumentType"
						v-model="inputDocumentType"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputDocumentNumber" class="col-sm-2 col-form-label"
					>Número Documento</label
				>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputDocumentNumber"
						v-model="inputDocumentNumber"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputEmail" class="col-sm-2 col-form-label"
					>Correo Electrónico</label
				>
				<div class="col-sm-10">
					<input
						type="email"
						class="form-control"
						id="inputEmail"
						v-model="inputEmail"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputFirstName" class="col-sm-2 col-form-label"
					>Nombres</label
				>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputFirstName"
						v-model="inputFirstName"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputLastName" class="col-sm-2 col-form-label"
					>Apellidos</label
				>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputLastName"
						v-model="inputLastName"
						required
					/>
				</div>
			</div>
			<button class="btn btn-xs btn-primary" @click="requestSubscriptionToken">
				Crear Suscripción
			</button>
			<!--<div v-show="callbackFail || callbackSuccess" class="row my-5">
				<div
					class="alert"
					:class="{
						'alert-danger': callbackFail,
						'alert-info': callbackSuccess,
					}"
					role="alert"
				>
					{{ callbackMessage }}
				</div>
			</div>-->
		</div>
	</div>
</template>

<script>
export default {
	name: "CreateSubscription",
	props: {
		msg: String,
	},
	data() {
		return {
			inputToken: "",
			inputPlanName: "",
			inputDocumentType: "",
			inputDocumentNumber: "",
			inputEmail: "",
			inputFirstName: "",
			inputLastName: "",
		};
	},
	methods: {},
};
</script>
