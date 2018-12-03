	<template>
		<div class="container">
			<form class="pt-3" @submit.prevent="onSubmit">
				<div class="form-group">
					<label for="name">Name</label>
					<input
					type="text"
					id="name"
					class="form-control"
					:class="{'is-invalid': $v.name.$error}"
					@blur="$v.name.$touch()"
					v-model="name"
					>
					<div class="invalid-feedback" v-if="!$v.name.required">Name field is required</div>
					<div class="invalid-feedback" v-if="!$v.name.minLength">Name must have at least {{$v.name.$params.minLength.min}} letters.</div>
				</div>
				<div class="form-group">
					<label for="phone">Phone</label>
					<input
					type="tel"
					id="phone"
					class="form-control"
					:class="{'is-invalid': $v.phone.$error}"
					@blur="$v.phone.$touch()"
					v-model="phone"
					maxlength="16"
					>
					<div class="invalid-feedback" v-if="!$v.phone.required">Phone field is required</div>
					<div class="invalid-feedback" v-if="!$v.phone.fullNumber">Phone number must have at least 11 numbers.</div>
				</div>
				<div class="form-group">
					<label for="message">Message</label>
					<textarea
					id="message"
					class="form-control"
					:class="{'is-invalid': $v.message.$error}"
					@blur="$v.message.$touch()"
					@input="$v.message.$touch()"
					v-model="message"
					/>
					<div>Number of characters: {{length}}</div>
					<div class="invalid-feedback" v-if="!$v.message.required">Message field is required</div>
					<div class="invalid-feedback" v-if="!$v.message.maxLength">Message must have at most {{$v.message.$params.maxLength.max}} charters.</div>
				</div>
				<button
				class="btn btn-success"
				type="submit"
				:disabled="$v.$invalid"
				>Submit</button>
			</form>
			<div class="row mt-4">
				<div class="col-lg-12">
					<div id="output"></div>
				</div>
			</div>
		</div>
	</template>

	<script>
		import { required, minLength, maxLength } from 'vuelidate/lib/validators';
		import Inputmask from 'inputmask';
		export default {
			data () {
				return {
					name: '',
					phone: '',
					message: ''
				}
			},
      computed: {
        length: function () {
          return this.message.length;
        }
      },
			validations: {
				name: {
					required,
					minLength: minLength(3)
				},
				phone: {
					required,
					minLength: minLength(16),
					fullNumber: function (number) {
						var foundPos = number.indexOf('_');
						if (foundPos === -1) return true;
						if (foundPos !== -1) return false;
					}
				},
				message: {
					required,
					maxLength: maxLength(250),
				}
			},
			mounted () {
				var im = new Inputmask("+7(999)999-99-99");
				im.mask(document.getElementById('phone'));
				if (localStorage.name) {
					this.name = localStorage.name;
				}
				if (localStorage.phone) {
					this.phone = localStorage.phone;
				}
				if (localStorage.message) {
					this.message = localStorage.message;
				}
			},
			methods: {
				onSubmit () {
					const axios = require('axios')
					var url = 'response.json'
					axios.post(url, this.name)
					.then(function (res) {
						output.className = 'text-success';
						output.innerHTML = res.data.response;
						setTimeout(function() {
							output.className = '';
							output.innerHTML = '';
						}, 2000)
					})
					.catch(function (err) {
						output.className = 'text-danger';
						output.innerHTML = err.message;
						setTimeout(function() {
							output.className = '';
							output.innerHTML = '';
						}, 2000)
					});
					localStorage.name = this.name;
					localStorage.phone = this.phone;
					localStorage.message = this.message;
				}
			},
		}
	</script>
