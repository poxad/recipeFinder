<script>
import feather from "feather-icons";

export default {
	name: "Home",
	data: () => {
		return {
			theme: "",
		};
	},
	created() {
		this.theme = localStorage.getItem("theme") || "light";
	},
	mounted() {
		feather.replace();
		this.theme = localStorage.getItem("theme") || "light";
	},
	updated() {
		feather.replace();
	},
	methods: {},
};
</script>
<template>
	<!-- Banner left contents -->
	<div class="w-full md:w-3/3 text-center">
		<h1
			class="font-general-semibold text-3xl md:text-3xl xl:text-4xl text-center sm:text-center text-ternary-dark dark:text-primary-light uppercase"
		>
			What food are you craving today?
		</h1>
	</div>
	
</template>

<style scoped>
/* Add any additional styling you need */
</style>

<style scoped></style>
