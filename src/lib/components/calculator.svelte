<script>
  let { challengeDay, monthDays, month, showTotal } = $props();

  const calculate = (calculateTotal = false) => {
    let pennies = challengeDay;
    let pounds = 0;
    let totalPennies = 1;

    if (calculateTotal) {
      for (let day = 1; day < Number(challengeDay); day++) {
        totalPennies += (day + 1);
      }

      pounds = (totalPennies / 100);
    }
    else {
      for (let day = 1; day < Number(monthDays); day++) {
        pennies += (Number(challengeDay) + day);
      }

      pounds = (pennies / 100);
    }

    // Convert the amount to a decimal so we can format as a currency.
    return new Intl.NumberFormat('en-GB', {
      style: 'currency',
      currency: 'GBP'
    }).format(pounds);
  }

  let total = $derived(calculate());
  let totalAccumulated = $derived(calculate(showTotal))
</script>

{#if challengeDay > 0 }
  <div class="my-10 bg-blue-800 py-3 px-5">
    <p class="text-lg"><strong class="text-blue-500">{total}</strong> will be taken for the challenge during the month of {month}.</p>

    {#if showTotal}
      <p class="mt-5 text-lg inline-block">You've saved a total of <strong class="text-blue-500">{totalAccumulated}</strong> so far! (minus any interest earnt)</p>
    {/if}
  </div>
{/if}

