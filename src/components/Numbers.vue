<script setup lang="ts">
import { ref, watch } from "vue";

//The maximum number in the list
const limit = ref(100);

//The selected number
//From which to get the factors
const selectedNumber = ref(-1);

//The shuffled array of numbers up to `limit`
const numbers = ref(createAndShuffleNumbers(limit.value));

//Regenerate and shuffle the list of numbers when the limit is updated
watch(limit, (v) => {
	numbers.value = createAndShuffleNumbers(v);
});

/**
 * Create an array of numbers in the range 1..max (inclusive) and return it shuffled in a random order.
 * @param max The largest value to include in the array
 */
function createAndShuffleNumbers(max: number): number[] {
	//Create a list of numbers from 1 to 100 (inclusive) by doing the following:
	//Create an empty array of length 100
	//Then set each index's value to it's position in the list (1-indexed)
	let arr = Array.from({ length: max }).map((_, i) => i + 1);

	//Randomise the order of the list
	arr.sort(() => Math.random() - 0.5);

	return arr;
}

/**
 * Update the value used to determine the factors.
 * @param number	The number to select
 */
function selectNumber(number: number) {
	selectedNumber.value = number;
}

/**
 * Clear the number selection
 */
function resetNumberSelection() {
	selectedNumber.value = -1;
}
</script>

<template>
	<div>
		<input type="number" v-model="limit"/>

		<br/>
		<br/>

		<div
			v-for="number in numbers"
			:key="number"
			:class="{
				'number': true,
				'active': (selectedNumber !== -1 && selectedNumber % number === 0)
        	}"
			@mouseover="selectNumber(number)"
			@mouseout="resetNumberSelection"
			v-text="number"
		></div>
	</div>
</template>

<style>
.number {
	display: inline-block;
	padding: 5px;
	background-color: lightgrey;
	margin: 5px;
}

.active {
	background-color: red;
}
</style>
