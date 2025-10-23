<script>
	import Calculator from './calculator.svelte';
	
	let challengeDay = $state(0);
	let total = $state(0);
	const months = ([
			{days: 31, name: 'January', id: 0},
			{days: 28, name: 'February', id: 1},
			{days: 31, name: 'March', id: 2},
			{days: 30, name: 'April', id: 3},
			{days: 31, name: 'May', id: 4},
			{days: 30, name: 'June', id: 5},
			{days: 31, name: 'July', id: 6},
			{days: 31, name: 'August', id: 7},
			{days: 30, name: 'September', id: 8},
			{days: 31, name: 'October', id: 9},
			{days: 30, name: 'November', id: 10},
			{days: 31, name: 'December', id: 11},
	]);

	// Get the current month
	const date = new Date();
	const month = date.getMonth();
	const currentMonth = months.find(m => m.id === month);

	// Get data about the month that was selected in the drop down
	let selectedMonth = $state(currentMonth.id);
	let selectedMonthData = $derived(months.find(m => m.id === selectedMonth));

	function resetCalculator() {
		challengeDay = 0;
		total = 0;
		selectedMonth = currentMonth.id;
	}

</script>

<div class="mx-auto flex flex-col gap-10 justify-center mt-20 mb-12 xl:mb-30">
	<div class="flex flex-wrap items-center gap-4">
		<label for="currentDay" class="sr-only">Current day</label>
		<input name="currentDay" type="text" bind:value={challengeDay} placeholder="Current day of your challenge">
		<div class="text-sm">Enter the current day of your challenge, so if you're paying £1.23 today, that means you're on day 123.</div>
	</div>
	<div class="flex flex-wrap items-center gap-4">
		<label for="month" class="sr-only">Month</label>
		<select name="month" bind:value={selectedMonth}>
			{#each months as month}
				<option value={month.id}>{month.name}</option>
			{/each}
		</select>
		<div class="text-sm">The month you want to calculate for (assumes the start of the month).</div>
	</div>

	<Calculator challengeDay={challengeDay} monthDays={selectedMonthData.days} month={selectedMonthData.name} total={total} />
</div>
<div>
	<button class="cursor-pointer block" onclick={resetCalculator}>Reset</button>
</div>
