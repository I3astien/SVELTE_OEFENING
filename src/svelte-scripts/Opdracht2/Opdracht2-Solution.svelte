<!--
FEEDBACK FOR BAS:

What he did well:
- All three functions work correctly (increment, decrement, reset)
- Clean component structure
- Good use of count++ and count-- operators
- Nice button layout with flexbox

What he did wrong:
- Missed the challenge requirement: text color should change based on count value
- Still using lang="scss" without SCSS installed (repeated from Opdracht 1)
- Didn't use ternary operators for the color logic

Concepts he struggled with:
- Implementing conditional styling with ternary operators
- Nested ternary operators (positive/negative/zero check)

What needs reinforcement in future assignments:
- Ternary operators for conditional rendering/styling
- Inline styles in Svelte
- Reading all requirements carefully (especially challenge sections)
-->

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

  // Helper function to get the color (alternative approach)
  function getColor() {
    return count > 0 ? 'green' : count < 0 ? 'red' : 'white'
  }
</script>

<div class="container">
  <!-- Using inline style with ternary operator -->
  <p
    class="count"
    style="color: {count > 0 ? 'green' : count < 0 ? 'red' : 'white'}"
  >
    Count: {count}
  </p>

  <div class="button-wrapper">
    <button on:click={subtractCount}>-</button>
    <button class="reset" on:click={resetCount}>Reset</button>
    <button on:click={addCount}>+</button>
  </div>
</div>

<style>
  .container {
    padding: 1rem;
    text-align: center;
  }

  .count {
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 1.5rem;
  }

  .button-wrapper {
    display: flex;
    justify-content: center;
    gap: 1rem;
  }

  button {
    background-color: rgb(48, 86, 48);
    color: white;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
    min-width: 60px;
  }

  button:hover {
    background-color: rgb(60, 100, 60);
  }

  button.reset {
    background-color: rgb(86, 48, 48);
  }

  button.reset:hover {
    background-color: rgb(100, 60, 60);
  }
</style>
