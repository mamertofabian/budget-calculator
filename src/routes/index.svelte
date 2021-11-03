<script lang="ts">
  import { setContext } from "svelte";
  import Navbar from "../components/Navbar.svelte";
  import ExpenseList from "../components/ExpenseList.svelte";
  import expensesData, { ExpenseInterface } from "../modules/expenses";
  import type { StateInterface } from "../modules/interfaces";

  const removeExpense = (id: number) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const state: StateInterface = {
    name: "just a name",
    removeExpense,
  };

  let expenses: ExpenseInterface[] = [...expensesData];

  setContext("state", state);
</script>

<Navbar />

<main class="content">
  <ExpenseList {expenses} />
</main>

<style>
</style>
