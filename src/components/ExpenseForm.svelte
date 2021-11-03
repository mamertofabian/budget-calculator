<script lang="ts">
  import Title from './Title.svelte';

  let name = '';
  let amount = null;
  export let addExpense;

  // $: console.log({name, amount});
  $: isEmpty = !name || !amount;

  const handleSubmit = () => {
    // using object parameter {} takes advantage of ES6 feature when the property name and the variable name is the same,
    // we can use the shorthand. + no need to worry about the order.
    addExpense({name, amount});
    name = '';
    amount = null;
  };
</script>

<section class="form">
  <Title title="add expense"/>
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" id="name" bind:value={name}>
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" id="amount" bind:value={amount}>
    </div>
    {#if isEmpty}
      <p class="form-empty">Please fill out all form fields</p>
    {/if}
    <button type="submit" class="btn btn-block" class:disabled={isEmpty} disabled={isEmpty}>
      Add Expense
    </button>
  </form>
  <button type="button" class="close-btn"><i class="fas fa-times"></i> Close</button>
</section>
