<script setup lang="ts">
import { ref, watch } from "vue";

const limit = ref(100);

const numbers = ref([] as number[]);

createAndShuffleNumbers(limit.value);

function createAndShuffleNumbers(max: number) {
	//Create a list of numbers from 1 to 100 (inclusive) by doing the following:
	//Create an empty array of length 100
	//Then set each index's value to it's position in the list (1-indexed)
	let arr = Array.from({ length: max }).map((_, i) => i + 1);

	//Randomise the order of the list
	arr.sort(() => Math.random() - 0.5);

	numbers.value = arr;
}

watch(limit, (v) => {
	createAndShuffleNumbers(v);
});

let selectedNumber = ref(-1);

function hov(number: number) {
	selectedNumber.value = number;
}

function reset() {
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
			@mouseover="hov(number)"
			@mouseout="reset"
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
