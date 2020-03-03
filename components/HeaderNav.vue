<template><div>
	<b-navbar class="header-nav-vue" toggleable="lg" type="light">
		<div class="container">
			<nuxt-link class="navbar-brand" to="/">Skambo</nuxt-link>
			<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

			<b-collapse id="nav-collapse" is-nav>
				<b-navbar-nav>
					<nuxt-link class="nav-link" to="/auth" v-if="!user">Auth</nuxt-link>
					<nuxt-link class="nav-link" to="/search">Search</nuxt-link>
					<nuxt-link class="nav-link" to="/settings">Settings</nuxt-link>
					<nuxt-link class="nav-link" to="/test">Test</nuxt-link>
				</b-navbar-nav>

				<!-- Right aligned nav items -->
				<b-navbar-nav class="ml-auto">
					<b-nav-form>
						<div class="input-group">
							<input type="text" class="form-control" placeholder="Search...">
							<div class="input-group-btn">
								<button type="submit" class="btn btn-primary">Go</button>
							</div>
						</div>
					</b-nav-form>

					<b-nav-item-dropdown right v-if="user">
						<!-- Using 'button-content' slot -->
						<template v-slot:button-content>
						<em>{{ user.displayName||user.email }}</em>
						</template>
						<nuxt-link class="dropdown-item" to="/settings">Settings</nuxt-link>
						<b-dropdown-item href="#" @click="logout();">Sign Out</b-dropdown-item>
					</b-nav-item-dropdown>
				</b-navbar-nav>
			</b-collapse>
		</div>
	</b-navbar>
	<br>
</div></template>

<script>
import firebase from 'firebase';

export default {
	data() {
		return {
			user: null,
		};
	},

	methods: {
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
.header-nav-vue {
	box-shadow:0px 0px 10px 0px #00000055;
}

.header-nav-vue .input-group {
	background:#ffffff;
	border: solid 1px #ddd;
}

.header-nav-vue .input-group .form-control,
.header-nav-vue .input-group .btn {
	background:none;
	border:none;
	color:#444;
	outline:0!important;
	box-shadow:none !important;
}

/*.header-nav-vue .navbar-collapse {
	position: fixed;
	right: 0px;
	top: 0px;
	width: 300px;
	height: 100%;
	background: #fff;
	padding: 15px;
	box-shadow:0px 0px 10px 0px #00000055;
}*/
</style>
