<script>
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";

  import ExpenseItem from "./ExpenseItem.svelte";
  import SectionTitle from "./Title.svelte";

  export let expenses = [];
</script>

<section>
  <SectionTitle title="expense list" />
  <ul>
    {#each expenses as expense, index (expense.id)}
      <div
        in:fly={{ x: 200, delay: index * 400 }}
        out:fly={{ x: -200 }}
        animate:flip>
        <ExpenseItem {...expense} />
      </div>
    {:else}
      <h2>No expenses added to the list!</h2>
    {/each}
  </ul>
</section>
