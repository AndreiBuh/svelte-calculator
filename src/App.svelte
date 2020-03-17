<script>
  import { setContext, onMount, afterUpdate } from "svelte";
  //components
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Modal from "./Modal.svelte";
  //variables
  let expenses = [];
  //toggle Forms
  let isModalOpen = false;
  //edit
  let updateId = null;
  let updateName = "";
  let updateAmount = null;
  //reactive
  $: isEditing = updateId ? true : false;
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator += current.amount);
  }, 0);

  //functions
  const showModal = () => {
    isModalOpen = true;
  };

  const hideModal = () => {
    isModalOpen = false;
    updateName = "";
    updateAmount = null;
    setId = null;
  };

  const removeExpense = id => {
    expenses = expenses.filter(expense => expense.id !== id);
  };

  const clearExpenses = () => {
    expenses = [];
  };

  const addExpense = ({ name, amount }) => {
    let newExpense = {
      id: Math.random() * Date.now(),
      name,
      amount
    };
    expenses = [newExpense, ...expenses];
  };

  const updateExpense = id => {
    let expense = expenses.find(expense => expense.id === id);
    updateId = expense.id;
    updateName = expense.name;
    updateAmount = expense.amount;
    showModal();
  };

  const editExpense = ({ name, amount }) => {
    expenses = expenses.map(expense => {
      return expense.id === updateId
        ? { ...expense, name, amount }
        : { ...expense };
    });
    updateId = null;
    updateAmount = null;
    updateName = "";
  };

  //context
  setContext("remove", removeExpense);
  setContext("update", updateExpense);

  //local storage
  const setLocalStorage = () => {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  };

  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });

  afterUpdate(() => {
    setLocalStorage();
  });
</script>

<Navbar {showModal} />

<main class="content">
  {#if isModalOpen}
    <Modal>
      <ExpenseForm
        {addExpense}
        name={updateName}
        amount={updateAmount}
        {isEditing}
        {editExpense}
        {hideModal} />
    </Modal>
  {/if}
  <Totals title="Total Expenses" {total} />
  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>
    clear expenses
  </button>
</main>
