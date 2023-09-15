<script>
import { CModal, CModalBody } from "@coreui/vue";

export default {
	props: ["project"],
	data() {
		return {
			result: [],
			modalVisible: false, // Data property to control modal visibility

			apiKey: "c586a88813394225a6bb560d838eb03b",
		};
	},
	methods: {
		async openModal() {
			// Simulate loading for 1 second
			await this.getInfo(this.project.id);

			this.modalVisible = true; // Show modal
		},
		closeModal() {
			// Function to close the modal
			this.modalVisible = false;
		},
		async getInfo(id) {
			try {
				const response = await fetch(
					`https://api.spoonacular.com/recipes/${id}/information?includeNutrition=false&apiKey=${this.apiKey}`
				);
				const data = await response.json();
				this.result = data;
				console.log(this.result.analyzedInstructions[0].steps);
			} catch (error) {
				console.error(error);
			}
		},
	},
	components: {
		CModal,

		CModalBody,
	},
};
</script>

<template>
	<!-- <router-link
		to="/projects/recipe-information"
		class="rounded-xl shadow-lg hover:shadow-xl cursor-pointer mb-10 sm:mb-0 bg-secondary-light dark:bg-ternary-dark"
		aria-label="Recipe Information" 
	
	> -->
	<div
		class="rounded-xl shadow-lg hover:shadow-xl cursor-pointer mb-10 sm:mb-0 bg-secondary-light dark:bg-ternary-dark"
		@click="openModal()"
	>
		<div>
			<img
				:src="project.image"
				:alt="project.title"
				class="rounded-t-xl border-none"
			/>
		</div>
		<div class="text-center px-4 py-6">
			<p
				class="font-general-semibold text-xl text-ternary-dark dark:text-ternary-light font-semibold mb-2"
			>
				{{ project.title }}
			</p>
			<span
				class="font-general-medium text-lg text-ternary-dark dark:text-ternary-light"
				>Click for more details</span
			>
		</div>
		<!-- </router-link> -->
	</div>
	<CModal size="xl" scrollable :visible="modalVisible" @close="closeModal()">
		<div class="modal-header">
			<h5
				class="modal-title"
				style="font-size: 24px; /* Font size */
			font-weight: bold; /* Font weight */
			text-align: left; /* Text"
			>
				{{ project.title }}
			</h5>
			<button
				type="button"
				class="close"
				aria-label="Close"
				@click="closeModal()"
				style="font-size: 30px"
			>
				<span aria-hidden="true">&times;</span>
			</button>
		</div>
		<CModalBody>
			<div style="text-align: left; display: flex">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					height="1em"
					viewBox="0 0 512 512"
					style="margin-top: 2px"
				>
					<!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
					<path
						d="M47.6 300.4L228.3 469.1c7.5 7 17.4 10.9 27.7 10.9s20.2-3.9 27.7-10.9L464.4 300.4c30.4-28.3 47.6-68 47.6-109.5v-5.8c0-69.9-50.5-129.5-119.4-141C347 36.5 300.6 51.4 268 84L256 96 244 84c-32.6-32.6-79-47.5-124.6-39.9C50.5 55.6 0 115.2 0 185.1v5.8c0 41.5 17.2 81.2 47.6 109.5z"
					/>
				</svg>
				&nbsp; {{ this.result.aggregateLikes }}
				people liked this recipe
			</div>
			<div
				v-html="this.result.summary"
				style="margin-top: 1%; margin-bottom: 2%; text-align: left"
			></div>

			<div style="text-align: left">Ingredients:</div>

			<div style="text-align: left; margin-top: 1%">
				<li v-for="ing in this.result.extendedIngredients" :key="ing.id">
					{{ ing.original }}
				</li>
			</div>

			<div style="text-align: left; margin-top: 2%">Instructions:</div>

			<div style="text-align: left; margin-top: 1%">
				<div
					v-for="step in this.result.analyzedInstructions"
					:key="step.number"
				>
					<p
						style="margin-top: 1%"
						v-for="(lol, index) in step.steps"
						:key="lol.name"
					>
						{{ index + 1 }}. {{ lol.step }}
					</p>
				</div>
			</div>
		</CModalBody>
	</CModal>
</template>

<style scoped>
@import "@coreui/coreui/dist/css/coreui.min.css";
@import "bootstrap/dist/css/bootstrap.min.css";
</style>
