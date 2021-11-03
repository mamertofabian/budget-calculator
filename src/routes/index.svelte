<script lang="ts">
  import { setContext } from 'svelte';
  import Navbar from '../components/Navbar.svelte';
  import ExpenseList from '../components/ExpenseList.svelte';
  import expensesData, { ExpenseInterface } from '../modules/expenses';
  import type { StateInterface } from '../modules/interfaces';
  import Totals from '../components/Totals.svelte';
  import ExpenseForm from '../components/ExpenseForm.svelte';

  interface Expense {
    name: string;
    amount: number;
  }

  const removeExpense = (id: number) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  let expenses: ExpenseInterface[] = [...expensesData];
  // set editing variables
  let setName = '';
  let setAmount = null;
  let setId = null;
  // toggle form variables
  let isFormOpen = false;
  // reactive
  $: isEditing = !!setId;
  $: total = expenses.reduce((acc, curr) => {
    console.log({acc, amount: curr.amount});
    return (acc + curr.amount)
  }, 0);

  const showForm = () => {
    isFormOpen = true;
  }

  const hideForm = () => {
    isFormOpen = false;
    setId = null;
    setName = '';
    setAmount = null;
  }

  const clearExpenses = () => {
    expenses = [];
  }

  const addExpense = ({name, amount}: Expense) => {
    const expense: ExpenseInterface = {id: Math.random() * Date.now(), name, amount}
    expenses = [expense, ...expenses];
  }

  const editExpense = ({name, amount}: Expense) => {
    expenses = expenses.map(item => {
      return item.id === setId ? {...item, name, amount} : item;
    });
    setId = null;
    setName = '';
    setAmount = null;
  }

  const setModifiedExpense = (id: number) => {
    const expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
  }

  const state: StateInterface = {
    setModifiedExpense,
    removeExpense,
  };
  setContext('state', state);
</script>

<Navbar {showForm}/>

<main class="content">
  {#if isFormOpen}
    <ExpenseForm {addExpense} name="{setName}" amount="{setAmount}" {isEditing} {editExpense} {hideForm}/>
  {/if}
  <Totals title="Total expenses" {total}/>
  <ExpenseList {expenses}/>
  <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>clear expenses</button>
</main>

<style>
</style>
