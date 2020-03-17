<script>
  export let showModal;
</script>

<nav class="nav">
  <div class="nav-center">
    <h1 class="nav-title">Budget calculator</h1>
    <button type="button" class="nav-btn" on:click={showModal}>
      <i class="far fa-plus-square" />
      add item
    </button>
  </div>
</nav>
