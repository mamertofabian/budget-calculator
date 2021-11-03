<script lang="ts">
  import { fly } from 'svelte/transition';
  import { flip } from 'svelte/animate'
  import Expense from './Expense.svelte';
  import type { ExpenseInterface } from '../modules/expenses';
  import SectionTitle from './Title.svelte';

  export let expenses: ExpenseInterface[] = [];
</script>

<section>
  <SectionTitle title="expense list"/>
  <ul>
    {#each expenses as expense, index (expense.id)}
      <div in:fly={{x:200, delay:(index + 1) * 200}} out:fly={{x:-200}} animate:flip>
        <Expense {...expense}/>
      </div>
    {:else}
      <h2>No expenses added to the list</h2>
    {/each}
  </ul>
</section>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>
