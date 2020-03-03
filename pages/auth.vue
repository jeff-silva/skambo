<template><div>
	<HeaderNav></HeaderNav>
	<AppAuth></AppAuth>
</div></template>

<script>
import HeaderNav from '~/components/HeaderNav.vue';
import AppAuth from '~/components/AppAuth.vue';
import firebase from 'firebase';

export default {
	data() {
		return {
			login: {
				email: '',
				pass: '',
			},
		};
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
	},

	components: {
		HeaderNav,
		AppAuth,
	},
}
</script>

<style scoped>
</style>