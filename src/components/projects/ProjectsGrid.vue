<script>
import feather from "feather-icons";
// import ProjectsFilter from './ProjectsFilter.vue';
import ProjectSingle from "./ProjectSingle.vue";
import projects from "../../data/projects";
export default {
	components: { ProjectSingle },
	data: () => {
		return {
			projects,
			projectsHeading: "Projects Portfolio",
			selectedCategory: "",
			searchProject: "",
			query: "",
			result: [],
			number: "",
			itemsPerPage: "20",
			dataNull: false,
			apiKey: "c586a88813394225a6bb560d838eb03b"
		};
	},
	computed: {
		isMobile() {
			return window.innerWidth <= 768; // Adjust the breakpoint as needed
		},
	},

	methods: {
		async fetchData() {
			try {
				const response = await fetch(
					`https://api.spoonacular.com/recipes/complexSearch?query=${this.query}&number=${this.itemsPerPage}&apiKey=${this.apiKey}`
				);
				const data = await response.json();
				this.result = data.results;	
				if (this.result.length === 0) {
					this.dataNull = true;
				} else {
					this.dataNull = false;
				}
			} catch (error) {
				console.error(error);
			}
		},
		increment() {
			this.itemsPerPage = Number(this.itemsPerPage) + 20;
			
			this.fetchData();
		},
	},
	mounted() {
		feather.replace();
	},
};
</script>

<template>
	<!-- Projects grid -->
	<section>
		<!-- Filter and search projects -->
		<div
			class="flex gap-2 align-center"
			style="text-align: center; justify-content: center; margin-top: 2%"
		>
			<input
				v-model="query"
				class="w-full lg:w-2/3 font-general-medium pl-3 pr-1 sm:px-4 py-2 border-1 border-gray-200 dark:border-secondary-dark rounded-lg text-sm sm:text-md bg-secondary-light dark:bg-ternary-dark text-primary-dark dark:text-ternary-light"
				id="name"
				@keyup.enter="fetchData()"
				name="name"
				type="search"
				required=""
				placeholder="Search Food Name"
				aria-label="Name"
			/>
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
		<div
			v-if="dataNull"
			class="font-general-semibold text-2xl md:text-2xl xl:text-2xl text-center sm:text-center text-ternary-dark dark:text-primary-light uppercase"
			style="text-align: center; margin-top: 5%"
		>
			Sorry, the recipe for this food is not available in our database..
		</div>
		<!-- Projects grid -->
		<div
			v-else
			class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 mt-6 sm:gap-10 py-12"
		>
			<ProjectSingle
				v-for="project in result"
				:key="project.id"
				:project="project"
			/>
		</div>
		<div v-if="!dataNull && (this.result.length!=0)">
			<button
				class="font-general-medium text-center text-md font-medium bg-indigo-500 hover:bg-indigo-600 text-white shadow-sm rounded-sm px-4 py-2 mt-2 duration-500"
				@click="increment()"
			>
				See more
			</button>
		</div>
	</section>
</template>

<style scoped></style>
