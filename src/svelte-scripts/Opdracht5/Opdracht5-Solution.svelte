<!--
FEEDBACK FOR BAS:

What he did well:
- Delete function works correctly with filter
- Using index in {#each} loop properly
- {#if} and {:else} blocks work great
- Good use of arrow function for onClick
- Read all requirements this time!

What he did wrong:
- Manually tracking totalTodoItems with ++ and -- is unnecessary
- Should use todos.length directly (Svelte reactivity handles it!)
- Forgot ternary operator for singular/plural text (challenge requirement)
- Creating redundant state that can be derived from existing data

Concepts he struggled with:
- Understanding derived/computed values in Svelte
- Trusting Svelte's reactivity (todos.length auto-updates!)
- Still forgot the ternary operator challenge (needs more practice)

What needs reinforcement in future assignments:
- Don't manually track what Svelte can compute automatically
- Use .length directly instead of separate counters
- Ternary operators (keep practicing!)
- Reactive statements for computed values
-->

<script>
  let todos = []
  let newTodo = ''

  function addTodo() {
    if (!newTodo) return
    todos = [...todos, newTodo]
    newTodo = ''
  }

  function removeTodo(index) {
    todos = todos.filter((_, i) => i !== index)
  }
</script>

<div class="container">
  <h2>Your Todos ({todos.length})</h2>

  {#if todos.length === 0}
    <p class="empty-message">No todos yet! Add one above.</p>
  {:else}
    <ul>
      {#each todos as todo, index}
        <li>
          <span class="todo-text">{todo}</span>
          <button class="delete-btn" on:click={() => removeTodo(index)}>×</button>
        </li>
      {/each}
    </ul>
  {/if}

  <div class="input-wrapper">
    <input
      type="text"
      bind:value={newTodo}
      placeholder="Enter a new todo..."
    />
    <button on:click={addTodo}>Add</button>
  </div>

  <p class="count">
    {#if todos.length === 0}
      You have 0 todos
    {:else}
      You have {todos.length === 1 ? '1 todo' : `${todos.length} todos`}
    {/if}
  </p>
</div>

<style lang="scss">
  .container {
    padding: 1rem;
    max-width: 500px;
    margin: 0 auto;
  }

  h2 {
    color: white;
    margin-bottom: 1rem;
    text-align: center;
  }

  .empty-message {
    color: rgba(255, 255, 255, 0.5);
    text-align: center;
    font-style: italic;
    padding: 2rem;
  }

  ul {
    list-style: none;
    padding: 0;
    margin-bottom: 1.5rem;

    li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      color: white;
      padding: 0.75rem;
      margin-bottom: 0.5rem;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 4px;

      .todo-text {
        flex: 1;
      }

      .delete-btn {
        background-color: rgb(86, 48, 48);
        color: white;
        border: none;
        border-radius: 4px;
        width: 30px;
        height: 30px;
        cursor: pointer;
        font-size: 1.2rem;
        line-height: 1;
        padding: 0;

        &:hover {
          background-color: rgb(120, 60, 60);
        }
      }
    }
  }

  .input-wrapper {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;

    input {
      flex: 1;
      padding: 0.5rem;
      border: 1px solid rgba(255, 255, 255, 0.3);
      border-radius: 4px;
      background-color: rgba(255, 255, 255, 0.05);
      color: white;

      &::placeholder {
        color: rgba(255, 255, 255, 0.5);
      }
    }

    button {
      background-color: rgb(48, 86, 48);
      color: white;
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 4px;
      cursor: pointer;

      &:hover {
        background-color: rgb(60, 100, 60);
      }
    }
  }

  .count {
    color: rgba(255, 255, 255, 0.7);
    text-align: center;
    font-style: italic;
  }
</style>
