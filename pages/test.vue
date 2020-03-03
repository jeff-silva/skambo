<template><div>
	<HeaderNav></HeaderNav>
	<div class="container">
		<h2>Test</h2>
		<button type="button" class="btn btn-primary" @click="apiTest();">{{ test }}</button>
		<pre>$data: {{ $data }}</pre>
	</div>
</div></template>

<script>
import HeaderNav from '~/components/HeaderNav.vue'
import axios from 'axios';

export default {
	data() {
		return {
			test: 'Click to reload',
		};
	},

	methods: {
		apiTest() {
			axios.get('./api/test').then((resp) => {
				this.test = `Random: ${resp.data.random}`;
			});
		}
	},

	components: {
		HeaderNav,
	},
}
</script>

<style scoped>

</style>