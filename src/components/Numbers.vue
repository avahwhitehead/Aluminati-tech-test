<script setup lang="ts">
let limit = 100;

function n() {
  //Create a list of numbers from 1 to 100 (inclusive)
  //Create an empty array of length 100
  //Then set each index's value to it's position in the list (1-indexed)
	let numbers: number[] = Array.from({length: 100}).map((_, i) => i + 1);

	return numbers.sort(() => Math.random() - 0.5);
}

function hov(number: number) {
  const nums = document.querySelectorAll('.number');

  for(let i = 0; i < nums.length; i++) {
    const num = nums[i].textContent.trim();
    if (number % num === 0) {
      nums[i].classList.add('active')
      console.log('divisor', num)
    }
  }
}

function reset() {
	const nums = document.querySelectorAll('.number');
	nums.forEach(num => num.classList.remove('active'))
}
</script>

<template>
	<div>
		<input type="number" v-model="limit" /><br /><br />
		<div class="number"
			:id="'number-'+number"
			v-for="number in n()"
			:key="number"
			@mouseover="hov(number)"
			@mouseout="reset"
		>
			{{ number }}
		</div>
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
