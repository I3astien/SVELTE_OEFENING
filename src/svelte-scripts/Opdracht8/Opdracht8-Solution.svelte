<!--
FEEDBACK FOR BAS:

What he did right:
- Correctly used immutable array updates (spread operator and filter) - EXCELLENT!
- Reactive statement for todo counter
- Proper remove function with index parameter
- Empty input validation
- Conditional rendering for counter messages
- Clean, well-structured code

What he did wrong:
- Variable naming: "InputValue" should be "inputValue" (camelCase)
- Redundant check: `empty === true` can just be `empty`
- Missing .trim() in validation - should check `InputValue.trim()` to catch spaces-only
- Empty message appears outside the list area instead of in place of the list
- Missing Enter key support (optional challenge)
- Layout quirk: ol with flex-direction column + align-items center looks odd

Concepts he struggled with:
- Minor: JavaScript naming conventions (camelCase for variables)
- Minor: Using .trim() for thorough input validation
- Minor: Structure/placement of conditional messages

What needs reinforcement in future assignments:
- Use .trim() when validating text input
- Follow camelCase for variable names
- Think about message placement in the UI flow
-->

<script>
  let todos = []
  let newTodo = ''

  // Reactive statement for todo count
  $: todoCount = todos.length

  // Reactive statement to check if input is empty
  $: isInputEmpty = newTodo.trim() === ''

  function addTodo() {
    if (newTodo.trim() !== '') {
      // Immutable array update - creates new array
      todos = [...todos, newTodo.trim()]
      newTodo = '' // Clear input
    }
  }

  function removeTodo(index) {
    // Filter creates a new array without the item at that index
    todos = todos.filter((_, i) => i !== index)
  }

  function handleKeydown(event) {
    if (event.key === 'Enter') {
      addTodo()
    }
  }
</script>

<div class="todo-app">
  <h2>My Todo List ({todoCount} {todoCount === 1 ? 'item' : 'items'})</h2>

  <div class="input-section">
    <input
      type="text"
      bind:value={newTodo}
      on:keydown={handleKeydown}
      placeholder="Enter a new todo..."
    />
    <button on:click={addTodo} disabled={isInputEmpty}>
      Add
    </button>
  </div>

  <div class="todo-list">
    {#if todos.length === 0}
      <p class="empty-message">No todos yet! Add one above.</p>
    {:else}
      {#each todos as todo, index}
        <div class="todo-item">
          <span class="bullet">•</span>
          <span class="todo-text">{todo}</span>
          <button class="remove-btn" on:click={() => removeTodo(index)}>
            Remove
          </button>
        </div>
      {/each}
    {/if}
  </div>
</div>

<style lang="scss">
  .todo-app {
    max-width: 500px;
    margin: 2rem auto;
    padding: 1.5rem;
    background: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

    h2 {
      margin-top: 0;
      color: #333;
    }
  }

  .input-section {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1.5rem;

    input {
      flex: 1;
      padding: 0.6rem;
      border: 2px solid #ddd;
      border-radius: 4px;
      font-size: 1rem;

      &:focus {
        outline: none;
        border-color: #4CAF50;
      }
    }

    button {
      padding: 0.6rem 1.2rem;
      background: #4CAF50;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1rem;
      font-weight: 500;

      &:hover:not(:disabled) {
        background: #45a049;
      }

      &:disabled {
        background: #ccc;
        cursor: not-allowed;
      }
    }
  }

  .todo-list {
    .empty-message {
      text-align: center;
      color: #999;
      font-style: italic;
      padding: 2rem 0;
    }
  }

  .todo-item {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.75rem;
    margin-bottom: 0.5rem;
    background: white;
    border-radius: 4px;
    border: 1px solid #e0e0e0;

    .bullet {
      color: #4CAF50;
      font-size: 1.2rem;
      font-weight: bold;
    }

    .todo-text {
      flex: 1;
      color: #333;
    }

    .remove-btn {
      padding: 0.4rem 0.8rem;
      background: #ff6b6b;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.9rem;

      &:hover {
        background: #ff5252;
      }
    }
  }
</style>
