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
			await this.getInfo(this.project.id);
			this.modalVisible = true; // Show modal
		},
		closeModal() {
			this.modalVisible = false; // Close modal
		},
		async getInfo(id) {
			try {
				const response = await fetch(
					`https://api.spoonacular.com/recipes/${id}/information?includeNutrition=false&apiKey=${this.apiKey}`
				);
				const data = await response.json();
				this.result = data;
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
	<div
		class="rounded-xl shadow-lg hover:shadow-xl cursor-pointer mb-10 sm:mb-0 bg-secondary-light dark:bg-ternary-dark border-container"
		@click="openModal()"
	>
		<div class="image-container">
			<img :src="project.image" :alt="project.title" class="image" />
		</div>
		<div class="text-container px-3 mb-3 flex flex-col justify-between">
			<p class="font-general-semibold text-sm text-ternary-dark dark:text-ternary-light font-semibold mb-2">
				{{ project.title }}
			</p>
			<span class="font-general-medium text-xs text-ternary-dark dark:text-ternary-light self-center mt-auto">
				Click for more details
			</span>
		</div>
	</div>

	<CModal size="lg" scrollable :visible="modalVisible" @close="closeModal()">
		<div class="modal-header">
			<h5 class="modal-title">
				{{ project.title }}
			</h5>
			<button
				type="button"
				class="close"
				aria-label="Close"
				@click="closeModal()"
			>
				<span aria-hidden="true">&times;</span>
			</button>
		</div>
		<CModalBody>
			<div class="modal-content">
				<div class="modal-meta">
					❤️ {{ this.result.aggregateLikes }} people liked this recipe
				</div>
				<div v-html="this.result.summary" class="modal-summary"></div>

				<div class="modal-columns">
					<div class="modal-column ingredients">
						<h6>Ingredients:</h6>
						<ul>
							<li v-for="ing in this.result.extendedIngredients" :key="ing.id" class="ingredient-item">
								• {{ ing.original }}
							</li>
						</ul>
					</div>
					<div class="modal-column steps">
						<h6>Instructions:</h6>
						<div v-for="step in this.result.analyzedInstructions" :key="step.number">
							<div v-for="(instruction, index) in step.steps" :key="instruction.name" class="instruction-step mb-3">
								<strong>Step {{ index + 1 }}:</strong> {{ instruction.step }}
							</div>
						</div>
					</div>
				</div>
			</div>
		</CModalBody>
	</CModal>
</template>

<style scoped>
@import "@coreui/coreui/dist/css/coreui.min.css";
@import "bootstrap/dist/css/bootstrap.min.css";

.border-container {
	border: 1px solid #dcdcdc; /* Light grey border */
	border-radius: 10px; /* Rounded corners */
}

.image-container img {
	padding: 10px;
	border-radius: 25px; /* Rounded corners for the image */
}

.text-container p {
	font-size: 14px; /* Smaller text size */
	text-align: left; /* Align text to the left */
}

.text-container {
	min-height: 85px; /* Adjust as needed */
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.text-container span {
	font-size: 12px; /* Smaller text size */
	text-align: left; /* Align text to the left */
}

.smaller-title {
	font-size: 20px;
	font-weight: bold;
	text-align: left;
}

.modal-content {
	padding: 20px;
}

.modal-header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding-bottom: 10px;
	border-bottom: 1px solid #e9ecef;
}

.modal-title {
	font-size: 24px;
	font-weight: bold;
}

.close {
	font-size: 30px;
	color: #333;
	background: none;
	border: none;
	cursor: pointer;
}

.modal-meta {
	font-size: 14px;
	color: #6c757d;
	margin-bottom: 10px;
}

.modal-summary {
	margin-top: 10px;
	margin-bottom: 20px;
}

.modal-columns {
	display: grid;
	grid-template-columns: 1fr 2fr; /* Left column narrower, right column wider */
	gap: 20px;
}

.modal-column {
	padding: 10px;
	background: #f8f9fa;
	border-radius: 8px;
}

.ingredients {
	background-color: #fff; /* White background for ingredients */
}

.steps {
	background-color: #fff; /* White background for steps */
}

h6 {
	font-size: 18px; /* Header size for ingredients and steps */
	font-weight: bold;
	margin-bottom: 10px;
}

.ingredient-item {
	text-align: left;
	padding: 5px; /* Padding inside each list item */
	margin-bottom: 5px; /* Space between list items */
}

.instruction-step {
	text-align:left;
	border: 1px solid #dcdcdc; /* 1px border for each ingredient */
	border-radius: 10px; /* Rounded corners for the border */
	margin-top: 5px;
	font-size: 16px;
}
</style>
