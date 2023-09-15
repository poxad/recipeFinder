<script>
export default {
	setup() {
		return {
			bios: [
				{
					id: 1,
					bio: "RecipeFinder is a leading online platform dedicated to culinary enthusiasts and food lovers worldwide. Established with a passion for making cooking an enjoyable and accessible experience, RecipeFinder has become a trusted name in the world of culinary exploration.",
				},
				{
					id: 2,
					bio: "Our mission at RecipeFinder is to empower individuals to discover, create, and share delightful culinary experiences from around the world. We aim to simplify the way people access, search, and enjoy diverse recipes, fostering a love for cooking and culinary exploration.",
				},
			],
		};
	},
};
</script>

<template>
	<div class="block sm:flex sm:gap-10 mt-10 sm:mt-20">
		<!-- About profile image -->

		<!-- About details -->
		<div class="w-full sm:w-4/4 text-center">
			<p
				v-for="bio in bios"
				:key="bio.id"
				class="font-general-regular mb-4 text-ternary-dark dark:text-ternary-light text-lg"
			>
				{{ bio.bio }}
			</p>
		</div>
	</div>
</template>
