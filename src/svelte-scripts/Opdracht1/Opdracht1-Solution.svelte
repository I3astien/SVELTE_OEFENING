<!--
FEEDBACK FOR BAS:

What he did well:
- Reactive variable works correctly
- Event handler connected properly
- Logic works (toggles between "Bas" and "World")
- Clean component structure

What he did wrong:
- Nested if statements were unnecessarily complex (could use ternary)
- Used lang="scss" without SCSS installed—styles won't work as expected
- BEM naming (.Name__text) is overkill for scoped Svelte components

Concepts he struggled with:
- Simplifying conditionals (ternary operator)
- Understanding Svelte's built-in CSS scoping

What needs reinforcement in future assignments:
- Ternary operators for simple conditions
- Basic CSS in Svelte (styles are scoped automatically)
-->

<script>
  let name = 'Bas'

  function nameChange() {
    name = name === 'Bas' ? 'World' : 'Bas'
  }
</script>

<div class="container">
  <p class="text">Hello {name}</p>
  <button on:click={nameChange}>Change Text!</button>
</div>

<style>
  .container {
    padding: 1rem;
  }

  .text {
    color: white;
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }

  button {
    background-color: rgb(48, 86, 48);
    color: white;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  button:hover {
    background-color: rgb(60, 100, 60);
  }
</style>
