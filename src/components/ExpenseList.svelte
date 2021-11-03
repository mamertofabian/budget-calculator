<script lang="ts">
  import Expense from "./Expense.svelte";
  import type { ExpenseInterface } from "../modules/expenses";
  import SectionTitle from "./Title.svelte";

  export let expenses: ExpenseInterface[] = [];
</script>

<section>
  <SectionTitle title="expense list" />
  <ul>
    {#each expenses as expense, index}
      <Expense {...expense} />
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
