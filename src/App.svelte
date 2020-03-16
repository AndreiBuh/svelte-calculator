<script>
  import { setContext } from "svelte";

  //components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  //data
  import expensesData from "./expenses";
  //variables
  let expenses = [...expensesData];
  //reactive
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator += current.amount);
  }, 0);
  //functions
  const removeExpense = id => {
    expenses = expenses.filter(expense => expense.id !== id);
  };

  const clearExpenses = () => {
    expenses = [];
  };
  //context
  setContext("remove", removeExpense);
</script>

<Navbar />

<main class="content">
  <ExpenseForm />
  <Totals title="Total Expenses" {total} />
  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>
    clear expenses
  </button>
</main>
