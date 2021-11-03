<script lang="ts">
  import { getContext } from 'svelte';
  import type { StateInterface } from '../modules/interfaces';

  export let id: number;
  export let name = '';
  export let amount = 0;
  let displayAmount = false;

  const toggleAmount = () => {
    displayAmount = !displayAmount;
  };

  const {removeExpense, setModifiedExpense} = getContext<StateInterface>('state');
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button on:click={toggleAmount} class="amount-btn"
      ><i
        class={displayAmount ? "fas fa-caret-up" : "fas fa-caret-down"}></i></button
      >
    </h2>
    {#if displayAmount}
      <h4>amount: ${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={() => setModifiedExpense(id)}>
      <i class="fas fa-pen"></i>
    </button>
    <button on:click={() => removeExpense(id)} class="expense-btn delete-btn">
      <i class="fas fa-trash"></i>
    </button>
  </div>
</article>
