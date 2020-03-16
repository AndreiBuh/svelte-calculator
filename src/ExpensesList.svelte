<script>
  import ExpenseItem from "./ExpenseItem.svelte";
  import SectionTitle from "./Title.svelte";

  export let expenses = [];
</script>

<section>
  <SectionTitle title="expense list" />
  <ul>
    {#each expenses as expense, index}
      <ExpenseItem {...expense} />
    {:else}
      <h2>No expenses added to the list!</h2>
    {/each}
  </ul>
</section>
