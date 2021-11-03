<script lang="ts">
  import { setContext } from 'svelte';
  import Navbar from '../components/Navbar.svelte';
  import ExpenseList from '../components/ExpenseList.svelte';
  import expensesData, { ExpenseInterface } from '../modules/expenses';
  import type { StateInterface } from '../modules/interfaces';
  import Totals from '../components/Totals.svelte';
  import ExpenseForm from '../components/ExpenseForm.svelte';

  const removeExpense = (id: number) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const state: StateInterface = {
    name: 'just a name',
    removeExpense,
  };

  let expenses: ExpenseInterface[] = [...expensesData];
  $: total = expenses.reduce((acc, curr) => {
    console.log({acc, amount: curr.amount});
    return (acc + curr.amount)
  }, 0);

  setContext('state', state);

  const clearExpenses = () => {
    expenses = [];
  }

  const addExpense = ({name, amount}) => {
    const expense = {id: Math.random() * Date.now(), name, amount}
    expenses = [expense, ...expenses];
  }
</script>

<Navbar/>

<main class="content">
  <ExpenseForm {addExpense} />
  <Totals title="Total expenses" {total}/>
  <ExpenseList {expenses}/>
  <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>clear expenses</button>
</main>

<style>
</style>
