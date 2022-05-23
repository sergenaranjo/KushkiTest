<template>
	<h1 class="my-5">Solicitud de Token de Suscripción</h1>
	<div class="card bg-light">
		<div class="card-body">
			<div class="mb-3 row">
				<label for="inputName" class="col-sm-2 col-form-label">Nombres</label>
				<div class="col-sm-10">
					<input
						type="text"
						class="form-control"
						id="inputName"
						v-model="inputName"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputNumber" class="col-sm-2 col-form-label"
					>Número Tarjeta</label
				>
				<div class="col-sm-10">
					<input
						type="text"
						maxlength="16"
						class="form-control"
						id="inputNumber"
						v-model="inputNumber"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputCVC" class="col-sm-2 col-form-label">CVC</label>
				<div class="col-sm-10">
					<input
						type="password"
						maxlength="3"
						class="form-control"
						id="inputCVC"
						v-model="inputCVC"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputExpiryMonth" class="col-sm-2 col-form-label"
					>Mes Expiración</label
				>
				<div class="col-sm-10">
					<input
						type="number"
						min="1"
						max="12"
						class="form-control"
						id="inputExpiryMonth"
						v-model="inputExpiryMonth"
						required
					/>
				</div>
			</div>
			<div class="mb-3 row">
				<label for="inputExpiryYear" class="col-sm-2 col-form-label"
					>Año Expiración</label
				>
				<div class="col-sm-10">
					<input
						type="number"
						min="2022"
						max="2050"
						class="form-control"
						id="inputExpiryYear"
						v-model="inputExpiryYear"
						required
					/>
				</div>
			</div>
			<button class="btn btn-xs btn-primary" @click="requestSubscriptionToken">
				Solicitar Token
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
/*
import { Kushki } from "@kushki/js";
*/

export default {
	name: "RequestToken",
	emits: ["sendToken"],
	props: {
		msg: String,
	},
	data() {
		return {
			callbackFail: false,
			callbackSuccess: false,
			callbackMessage: "",
			inputName: "",
			inputNumber: "",
			inputCVC: "",
			inputExpiryMonth: "",
			inputExpiryYear: "",
			token: "",
		};
	},
	methods: {
		requestSubscriptionToken(
		) {

			fetch("https://stoplight.io/mocks/api-kushki-docs/api-reference/59467660/subscriptions/v1/card/tokens", {
			"method": "POST",
			"headers": {
				"Content-Type": "application/json",
				"Public-Merchant-Id": "20000000108750050000"
			},
			"body": "{\"card\":{\"name\":\""+this.inputName+"\",\"number\":\""+this.inputNumber+"\",\"expiryMonth\":\""+this.inputExpiryMonth+"\",\"expiryYear\":\""+this.inputExpiryYear+"\",\"cvv\":\""+this.inputCVC+"\"},\"currency\":\"USD\"}"
			})
			.then((res) => res.json())
			.then((response) => {
				this.$emit("sendToken", response.token);
				this.callbackSuccess = true;
				this.callbackMessage = "Se ha asignado el token: "+response.token;
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

			/* Implementación por Kushki.js
			var callback = async (response) => {
				if (!response.code) {
					this.$emit("sendToken", response.token);
					this.callbackSuccess = true;
					this.callbackMessage = response.token;
					this.token = response.token;
				} else {
					this.$emit("sendToken", "No hay token");
					this.callbackFail = true;
					this.callbackMessage =
						"Error: " +
						response.error +
						". Code: " +
						response.code +
						". Message: " +
						response.message;
				}
			};

			kushki.requestSubscriptionToken(
				{
					card: {
						name: inputName,
						number: inputNumber,
						cvc: inputCVC,
						expiryMonth: inputExpiryMonth,
						expiryYear: inputExpiryYear,
					},
					currency: "USD",
				},
				callback
			);
			*/
		},
	},
};

/* Implementación por Kushki.js
var kushki = new Kushki({
	merchantId: "20000000108750050000",
	inTestEnvironment: true,
	regional: false,
});
*/
</script>
