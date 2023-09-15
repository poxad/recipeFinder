<script>
import feather from "feather-icons";
import Multiselect from "@vueform/multiselect";
import ProjectSingle from "../components/projects/ProjectSingle.vue";
export default {
	components: { Multiselect, ProjectSingle },
	name: "Projects",
	data() {
		return {
			apiKey: "c586a88813394225a6bb560d838eb03b",
			value: null,
			options: [
				"salt",
				"olive oil",
				"butter",
				"sugar",
				"water",
				"flour",
				"garlic",
				"eggs",
				"onion",
				"vanilla extract",
				"milk",
				"kosher salt",
				"lemon juice",
				"unsalted butter",
				"black pepper",
				"baking powder",
				"pepper",
				"salt and pepper",
				"egg",
				"brown sugar",
				"baking soda",
				"garlic cloves",
				"vegetable oil",
				"granulated sugar",
				"honey",
				"ground cinnamon",
				"ground pepper",
				"cream cheese",
				"parmesan cheese",
				"garlic powder",
				"carrots",
				"cinnamon",
				"oregano",
				"red onion",
				"heavy cream",
				"celery",
				"chicken",
				"sour cream",
				"vanilla",
				"sea salt",
				"green onions",
				"lime juice",
				"soy sauce",
				"powdered sugar",
				"fresh parsley",
				"bacon",
				"cornstarch",
				"ground cumin",
				"tomatoes",
				"canola oil",
				"oil",
				"chicken broth",
				"maple syrup",
				"red bell pepper",
				"canned tomatoes",
				"lemon zest",
				"paprika",
				"dijon mustard",
				"chili powder",
				"chocolate",
				"mayonnaise",
				"white sugar",
				"onions",
				"fresh cilantro",
				"parsley",
				"cilantro",
				"pecans",
				"beef",
				"ginger",
				"garlic clove",
				"red pepper flakes",
				"walnuts",
				"cayenne pepper",
				"extra virgin olive oil",
				"carrot",
				"coconut oil",
				"zucchini",
				"strawberries",
				"worcestershire sauce",
				"sesame oil",
				"food dye",
				"orange juice",
				"potatoes",
				"fish",
				"tomato",
				"juice of lemon",
				"avocado",
				"buttermilk",
				"light brown sugar",
				"nutmeg",
				"balsamic vinegar",
				"ground ginger",
				"yellow onion",
				"fresh ginger",
				"egg whites",
				"ground nutmeg",
				"shredded cheddar cheese",
				"green bell pepper",
				"almonds",
				"whole milk",
				"lemon",
				"shrimp",
				"tomato paste",
				"scallions",
				"onion powder",
				"all purpose flour",
				"chicken stock",
				"egg yolks",
				"cumin",
				"red wine vinegar",
				"confectioners' sugar",
				"shallots",
				"fresh basil",
				"ground beef",
				"spinach",
				"mushrooms",
				"blueberries",
				"rye meal",
				"fresh thyme",
				"bread",
				"peanut butter",
				"dried thyme",
				"skinless boneless chicken breasts",
			],
			result: [],
		};
	},

	methods: {
		addTag(newTag) {
			const tag = {
				name: newTag,
				code: newTag.substring(0, 2) + Math.floor(Math.random() * 10000000),
			};
			this.taggingOptions.push(tag);
			this.taggingSelected.push(tag);
		},
		async fetchData() {
			try {
				const valueString = this.value.join(",");
				console.log(valueString);
				const response = await fetch(
					`https://api.spoonacular.com/recipes/findByIngredients?apiKey=${this.apiKey}&number=50&ingredients=${valueString}`
				);
				const data = await response.json();
				this.result = data;
				console.log(this.result);
			} catch (error) {
				console.error(error);
			}
		},
	},
	mounted() {
		feather.replace();
	},
};
</script>

<template>
	<div class="container mx-auto">
		<div class="w-full md:w-3/3 text-center">
			<h1
				class="font-general-semibold text-3xl md:text-3xl xl:text-4xl text-center sm:text-center text-ternary-dark dark:text-primary-light uppercase"
			>
				Type the ingredients you want to use
			</h1>
		</div>
		<div
			class="flex gap-2 align-center"
			style="text-align: center; justify-content: center; margin-top: 2%"
		>
			<div class="relative w-full lg:w-2/3">
				<Multiselect
					v-model="value"
					mode="tags"
					:close-on-select="false"
					:searchable="true"
					:create-option="false"
					:options="options"
					class="multiselect-blue"
				/>
			</div>
			<span
				class="bg-primary-light dark:bg-ternary-dark p-2.5 shadow-sm rounded-xl cursor-pointer"
				@click="fetchData()"
			>
				<i
					data-feather="search"
					class="text-ternary-dark dark:text-ternary-light"
				></i>
			</span>
		</div>
		<!-- {{ this.result }} -->
		<div
			class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 mt-6 sm:gap-10 py-12"
		>
			<ProjectSingle
				v-for="recipe in result"
				:key="recipe.id"
				:project="recipe"
			/>
		</div>
	</div>
</template>

<style src="@vueform/multiselect/themes/default.css">
.multiselect-blue {
	--ms-tag-bg: #6366f1;
	--ms-tag-color: #6366f1;
}
</style>
