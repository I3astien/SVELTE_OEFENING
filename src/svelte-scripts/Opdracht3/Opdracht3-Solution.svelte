<!--
FEEDBACK FOR BAS:

What he did well:
- {#if} conditional rendering works perfectly
- Toggle function correctly flips boolean with !isVisible
- Clean component structure
- Nice extra touch creating a messageText variable

What he did wrong:
- Missed the challenge requirement: button text should change with ternary operator
- Started isVisible at true instead of false (minor)
- Used absolute positioning with percentage that might not work on all screen sizes

Concepts he struggled with:
- Using ternary operators in template (button text should change)
- Reading ALL requirements before coding (missed challenge again)

What needs reinforcement in future assignments:
- Ternary operators inside template expressions
- Reading requirements completely, especially challenge sections
- Keep layouts simple and responsive
-->

<script>
  let isVisible = false

  function toggleVisibility() {
    isVisible = !isVisible
  }
</script>

<div class="container">
  <button on:click={toggleVisibility}>
    {isVisible ? 'Hide Message' : 'Show Message'}
  </button>

  {#if isVisible}
    <div class="message">
      <p>Hello! This is a secret message.</p>
    </div>
  {/if}
</div>

<style lang="scss">
  .container {
    text-align: center;
    padding: 1rem;
  }

  button {
    background-color: rgb(48, 86, 48);
    color: white;
    padding: 0.5rem 1.5rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
    margin-bottom: 1rem;

    &:hover {
      background-color: rgb(60, 100, 60);
    }
  }

  .message {
    background-color: rgba(255, 255, 255, 0.1);
    padding: 1rem;
    border-radius: 8px;
    margin-top: 1rem;

    p {
      color: white;
      margin: 0;
      font-size: 1.1rem;
    }
  }
</style>
