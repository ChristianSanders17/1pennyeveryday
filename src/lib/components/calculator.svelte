<script>
  let { challengeDay, monthDays, month } = $props();

  
  const calculate = () => {
    let pennies = 0;

    for (let day = 1; day <= Number(monthDays); day++) {
      pennies += (Number(challengeDay) + day);
    }

    let pounds = (pennies / 100);

    // Convert the amount to a decimal so we can format as a currency.
    return new Intl.NumberFormat('en-GB', {
      style: 'currency',
      currency: 'GBP'
    }).format(pounds);
  }

  let total = $derived(calculate());
</script>

{#if challengeDay > 0 }
  <p class="text-lg"><strong class="text-blue-500">{total}</strong> will be taken for the challenge during the month of {month}.</p>
{/if}

