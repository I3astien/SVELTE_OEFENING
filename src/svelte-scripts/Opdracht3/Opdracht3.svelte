<script>
  let isVisible = true
  let messageText = 'Hello World!'

  function toggleVisibility() {
    isVisible = !isVisible
  }
</script>

<div class="wrapper">
  {#if isVisible}
    <div class="message">
      {messageText}
    </div>
  {/if}
  <div class="button">
    <button on:click={toggleVisibility}>Toggle Message!</button>
  </div>
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    justify-content: center;
    flex-direction: column;
    gap: 1rem;
    position: relative;

    .button {
      position: absolute;
      top: 3rem;
      left: 35%;
    }
  }
</style>
