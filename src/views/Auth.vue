<template><div>

	<div class="container">
		<div v-if="routePath=='/auth/login'">
			<form action="">
				<div class="form-group">
					<label>Email</label>
					<input type="text" class="form-control" v-model="login.email">
				</div>

				<div class="form-group">
					<label>Password</label>
					<input type="password" class="form-control" v-model="login.pass">
				</div>

				<br>
				<button type="submit" class="btn btn-primary btn-block">Login</button>
			</form>
		</div>

		<div v-else-if="routePath=='/auth/register'">
			<form action="">
				<div class="form-group">
					<label>Name</label>
					<input type="text" class="form-control" v-model="register.name">
				</div>

				<div class="form-group">
					<label>Email</label>
					<input type="text" class="form-control" v-model="register.email">
				</div>

				<div class="form-group">
					<label>Password</label>
					<input type="password" class="form-control" v-model="register.pass">
				</div>

				<div class="form-group">
					<label>Repeat password</label>
					<input type="password" class="form-control" v-model="register.repass">
				</div>

				<br>
				<button type="submit" class="btn btn-primary btn-block">Register</button>
			</form>
		</div>

		<div v-else-if="routePath=='/auth/password'">
			<form action="">
				<div class="form-group">
					<label>Email</label>
					<input type="text" class="form-control" v-model="password.email">
				</div>

				<div class="form-group">
					<label>Code</label>
					<input type="text" class="form-control" v-model="password.code">
				</div>

				<div class="form-group">
					<label>New Password</label>
					<input type="password" class="form-control" v-model="password.pass">
				</div>

				<div class="form-group">
					<label>Repeat password</label>
					<input type="password" class="form-control" v-model="password.repass">
				</div>

				<br>
				<button type="submit" class="btn btn-primary btn-block">Proceed</button>
			</form>
		</div>
		
		<br>
		<div class="list-inline">
			<router-link to="/auth/login" class="list-inline-item">Login</router-link>
			<router-link to="/auth/register" class="list-inline-item">Register</router-link>
			<router-link to="/auth/password" class="list-inline-item">Password</router-link>
		</div>
	</div>

	<!-- <pre>$data: {{ $data }}</pre> -->
</div></template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
	name: 'Auth',
	
	data() {
		return {
			routePath: '/auth/login',
			login: {
				email: '',
				pass: '',
			},
			register: {
				name: '',
				email: '',
				pass: '',
				repass: '',
			},
			password: {
				email: '',
				code: '',
				pass: '',
				repass: '',
			},
		};
	},

	watch: {
		$route: function(to, from) {
			this.routePath = to.path;
		},
	},
});
</script>

<style scoped>
</style>