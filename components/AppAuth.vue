<template><div>

	<div style="max-width:300px; margin:0 auto;">

		<!-- logged -->
		<div v-if="user">
			<div>Bem vindo {{ user.displayName||user.email }}.</div>
			<div><a href="#" @click="logout();">Sair</a></div>
		</div>

		<div v-if="!user">
			<!-- login -->
			<form action="" method="post" @submit.prevent="loginSubmit();" v-if="attrForm=='login'">
				<div class="form-group">
					<label>Email</label>
					<input type="email" class="form-control" v-model="login.email">
				</div>

				<div class="form-group">
					<label>Pass</label>
					<input type="password" class="form-control" v-model="login.pass">
				</div>

				<button type="submit" class="btn btn-primary btn-block">Login</button>
			</form>
			

			<!-- register -->
			<form action="" method="post" @submit.prevent="registerSubmit();" v-if="attrForm=='register'">
				<div class="form-group">
					<label>Email</label>
					<input type="email" class="form-control" v-model="register.email">
				</div>

				<div class="form-group">
					<label>Pass</label>
					<input type="password" class="form-control" v-model="register.pass">
				</div>

				<div class="form-group">
					<label>Repass</label>
					<input type="password" class="form-control" v-model="register.repass">
				</div>

				<button type="submit" class="btn btn-primary btn-block">Register</button>
			</form>
			

			<!-- password -->
			<form action="" method="post" @submit.prevent="passwordSubmit();" v-if="attrForm=='password'">
				<div class="form-group">
					<label>Email</label>
					<input type="email" class="form-control" v-model="password.email">
				</div>

				<div class="form-group">
					<label>Code</label>
					<input type="text" class="form-control" v-model="password.code">
				</div>

				<div class="form-group">
					<label>Pass</label>
					<input type="password" class="form-control" v-model="password.pass">
				</div>

				<div class="form-group">
					<label>Repass</label>
					<input type="password" class="form-control" v-model="password.repass">
				</div>

				<button type="submit" class="btn btn-primary btn-block">Password</button>
			</form>

			<br>
			<div class="list-inline">
				<a href="#" class="list-inline-item" @click="attrForm='login';">Login</a>
				<a href="#" class="list-inline-item" @click="attrForm='register';">Register</a>
				<a href="#" class="list-inline-item" @click="attrForm='password';">Password</a>
			</div>
		</div>
	</div>
</div></template>

<script>
import firebase from 'firebase';

export default {
	data() {
		return {
			attrForm: this.form,
			user: null,
			login: {
				email: '',
				pass: '',
			},
			register: {
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

	props: {
		form: {default:'login'},
	},

	methods: {
		loginSubmit() {
			firebase.auth().signInWithEmailAndPassword(this.login.email, this.login.pass)
				.then((a, b, c) => {
					console.log(a, b, c);
				})
				.catch((error) => {
					alert(error.message);
				});
		},


		registerSubmit() {
			alert('registerSubmit');
		},


		passwordSubmit() {
			alert('passwordSubmit');
		},


		logout() {
			firebase.auth().signOut()
				.then(() => {
					this.user = null;
				})
				.catch((error) => {
					alert(error.message);
				});
		},
	},

	mounted() {
		firebase.auth().onAuthStateChanged((user) => {
			this.user = user||null;
		});
	},
}
</script>

<style>

</style>