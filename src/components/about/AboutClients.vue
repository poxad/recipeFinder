<script>
// import AboutClientSingle from './AboutClientSingle.vue';

export default {
	components: {
		// AboutClientSingle,
	},
	data: () => {
		return {
			clientsHeading: "Key Features and Offerings",
		};
	},
};
</script>

<template>
	<div class="mt-10 sm:mt-20">
		<p
			class="font-general-medium text-2xl sm:text-3xl text-primary-dark dark:text-primary-light"
		>
			{{ clientsHeading }}
		</p>

		<p
			class="font-general-medium text-xl sm:text-xl text-primary dark:text-primary-light text-left mt-10"
		>
			1. <b>Extensive Recipe Database</b>: RecipeFinder boasts a vast and
			continuously expanding database of recipes from all corners of the globe.
			From traditional family dishes to modern, innovative creations, we have
			something to satisfy every palate.
		</p>

		<p
			class="font-general-medium text-xl sm:text-xl text-primary dark:text-primary-light text-left mt-10"
		>
			2. <b>User-Friendly Website</b>: Our website is designed with user
			convenience in mind. It offers a seamless and intuitive search experience,
			allowing users to quickly find recipes by cuisine, ingredients, dietary
			preferences, or meal type.
		</p>

		<p
			class="font-general-medium text-xl sm:text-xl text-primary dark:text-primary-light text-left mt-10"
		>
			3. <b>Free Access</b>: RecipeFinder is committed to providing free access
			to all its resources. We believe that everyone should have the opportunity
			to explore and enjoy diverse culinary traditions without any cost
			barriers.
		</p>

		<p
			class="font-general-medium text-xl sm:text-xl text-primary dark:text-primary-light text-left mt-10"
		>
			4. <b>Community and Sharing</b>: RecipeFinder encourages a sense of
			community among users. Our platform allows users to share their favorite
			recipes, cooking tips, and food experiences with others, fostering a
			supportive and engaging culinary community.
		</p>

		<p
			class="font-general-medium text-xl sm:text-xl text-primary dark:text-primary-light text-left mt-10"
		>
			5. <b>Regular Updates</b>: We are committed to keeping our recipe
			collection up-to-date with the latest culinary trends, seasonal
			ingredients, and dietary preferences.
		</p>
	</div>
</template>
