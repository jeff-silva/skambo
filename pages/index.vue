<template><div>
	<HeaderNav></HeaderNav>
	<div class="container">
		<h2>Bem vindo</h2>
	</div>
</div></template>

<script>
import HeaderNav from '~/components/HeaderNav.vue'

export default {
	data() {
		return {
			test: true,
		};
	},

	components: {
		HeaderNav,
	},
}
</script>

<style scoped>

</style>