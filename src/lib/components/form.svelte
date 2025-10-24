<script>
	import Calculator from './calculator.svelte';
	
	let challengeDay = $state();
	let showTotal = $state(false);
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

<div class="mx-auto flex flex-col gap-10 justify-center mb-10">
	<div class="flex flex-wrap items-center gap-4">
		<label for="currentDay" class="sr-only">Current day</label>
		<input name="currentDay" type="number" min="1" max="365" size="20" bind:value={challengeDay} placeholder="Current day of your challenge" class="max-w-[250px] w-full">
		<div class="text-sm">If you're paying £1.23 today, that means you're on day 123.</div>
	</div>
	<div class="flex flex-wrap items-center gap-4">
		<label for="month" class="sr-only">Month</label>
		<select id="month" name="month" bind:value={selectedMonth}>
			{#each months as month}
				<option value={month.id}>{month.name}</option>
			{/each}
		</select>
		<div class="text-sm">The month you want to calculate for (assumes the start of the month).</div>
	</div>
	<div class="flex flex-wrap items-center gap-4">
		<input type="checkbox" id="totalAccumulated" name="totalAccumulated" bind:checked={showTotal}>
		<label for="totalAccumulated" class="text-sm">Tick to show your total savings to date (day {challengeDay ? challengeDay : 1}).</label>
	</div>
</div>

<Calculator challengeDay={challengeDay} monthDays={selectedMonthData.days} month={selectedMonthData.name} showTotal={showTotal} />

<div>
	<button class="cursor-pointer block" onclick={resetCalculator}>Reset</button>
</div>
