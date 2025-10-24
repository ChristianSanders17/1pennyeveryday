<script>
	import Form from '../lib/components/form.svelte';
</script>

<div class="mx-auto w-full">
	<h1 class="mt-10 xl:mt-30 w-fit pb-4">The 1 Penny everyday challenge calculator</h1>
	<span class="block border-t border-b-blue-500 text-blue-500"></span>
	<p class="mt-5 mb-3">Some banks offer a challenge called the "1 penny everyday challenge". What this challenge does is it takes 1 penny from your current account on day 1. Each day increases by 1 penny. So day 2 is 2p, day 3 is 3p taken etc and so forth all the way up to day 365.</p>
	<p class="mb-3">The aim of this is to stop you spending money every month by taking alittle away from your account on a daily basis. The result? £667.95 will be waiting for you at the end of the challenge if you saved every day!</p>
	<p class="mb-10">This calculator helps you to know how many pennies will be taken from your account in any given month.</p>
	<Form />
</div>