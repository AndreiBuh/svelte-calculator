<script>
  import Title from "./Title.svelte";
  let name = "";
  let amount = null;

  $: isEmpty = !name || !amount;
</script>

<section class="form">
  <Title title="Add Expense" />
  <form class="expense-form">
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">Please fill out all form fields!</p>
    {/if}
    <button type="submit" class="btn btn-block">Add expense</button>
    <button type="button" class="close-btn">
      <i class="fa fa-times" />
      Close
    </button>
  </form>
</section>
