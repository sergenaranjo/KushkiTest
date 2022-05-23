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
			<button class="btn btn-xs btn-primary" @click="requestSubscription">
				Crear Suscripción
			</button>
			<div v-show="callbackFail || callbackSuccess" class="row my-5">
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
			</div>
		</div>
	</div>
</template>

<script>

import { toRef } from 'vue'

export default {
	name: "CreateSubscription",
	setup(props) {
	const token = toRef(props, 'token')
	return { token }
	},
	data() {
		return {
			callbackFail: false,
			callbackSuccess: false,
			callbackMessage: "",
			inputToken: "",
			inputPlanName: "",
			inputDocumentType: "",
			inputDocumentNumber: "",
			inputEmail: "",
			inputFirstName: "",
			inputLastName: "",
		};
	},
	created: function () {
		this.inputToken = this.token;
	},
	methods: {
		requestSubscription(
		) {

			fetch("https://stoplight.io/mocks/api-kushki-docs/api-reference/59467660/subscriptions/v1/card", {
			"method": "POST",
			"headers": {
				"Content-Type": "application/json",
				"Public-Merchant-Id": "20000000108750050000"
			},
			"body": "{\"token\":\""+this.inputToken+"\",\"planName\":\""+this.inputPlanName+"\",\"periodicity\":\"monthly\",\"contactDetails\":{\"documentType\":\""+this.inputDocumentType+"\",\"documentNumber\":\""+this.inputDocumentNumber+"\",\"email\":\""+this.inputEmail+"\",\"firstName\":\""+this.inputFirstName+"\",\"lastName\":\""+this.inputLastName+"\",\"phoneNumber\":\"+593912345678\"},\"amount\":{\"subtotalIva\":1,\"subtotalIva0\":0,\"ice\":0,\"iva\":0.14,\"currency\":\"USD\"},\"startDate\":\"2022-05-25\",\"metadata\":{\"plan\":{\"fitness\":{\"cardio\":\"include\",\"rumba\":\"include\",\"pool\":\"include\"}}}}"
			})
			.then((res) => res.json())
			.then((response) => {
				this.callbackSuccess = true;
				this.callbackMessage = "Se ha creado la suscripción con el ID: "+response.subscriptionId;
			})
			.catch(err => {
				this.callbackFail = true;
				this.callbackMessage =
					"Error: " +
					err.error +
					". Code: " +
					err.code +
					". Message: " +
					err.message;
			});
			/*
			fetch("https://stoplight.io/mocks/api-kushki-docs/api-reference/59467660/subscriptions/v1/card/tokens", {
			"method": "POST",
			"headers": {
				"Content-Type": "application/json",
				"Public-Merchant-Id": "20000000108750050000"
			},
			"body": {
				"card":{
					"name":inputName,
					"number":inputNumber,
					"expiryMonth":inputExpiryMonth,
					"expiryYear":inputExpiryYear,
					"cvv":inputCVC
				},
				"currency":"USD"
				}
			})
			.then(response => {
				this.$emit("sendToken", response.token);
				this.callbackSuccess = true;
				this.callbackMessage = response.token;
				this.token = response.token;			
			})
			.catch(err => {
				this.$emit("sendToken", "No hay token");
				this.callbackFail = true;
				this.callbackMessage =
					"Error: " +
					err.error +
					". Code: " +
					err.code +
					". Message: " +
					err.message;
			});
			*/
		},
	},
};
</script>
