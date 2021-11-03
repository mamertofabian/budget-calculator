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

  let expenses: ExpenseInterface[] = [...expensesData];
  // set editing variables
  let setName = '';
  let setAmount = null;
  let setId = null;
  // reactive
  $: total = expenses.reduce((acc, curr) => {
    console.log({acc, amount: curr.amount});
    return (acc + curr.amount)
  }, 0);

  const clearExpenses = () => {
    expenses = [];
  }

  const addExpense = ({name, amount}: {name: string, amount: number}) => {
    const expense: ExpenseInterface = {id: Math.random() * Date.now(), name, amount}
    expenses = [expense, ...expenses];
  }

  const setModifiedExpense = (id: number) => {
    const expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
  }

  const state: StateInterface = {
    setModifiedExpense,
    removeExpense,
  };
  setContext('state', state);
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
