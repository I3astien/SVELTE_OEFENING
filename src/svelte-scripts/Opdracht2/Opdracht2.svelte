<script>
  let count = 0
  function addCount() {
    count++
  }
  function subtractCount() {
    count--
  }
  function resetCount() {
    count = 0
  }
</script>

<p>This is the current count: {count}</p>

<div class="button-wrapper">
  <button on:click={subtractCount}>Subtract count!</button>
  <button on:click={resetCount}>Reset count!</button>
  <button on:click={addCount}>Add to count!</button>
</div>

<style lang="scss">
  .button-wrapper {
    display: flex;
    justify-content: center;
    gap: 2rem;

    button {
      background-color: rgb(48, 86, 48);
      color: white;
    }
  }
</style>
