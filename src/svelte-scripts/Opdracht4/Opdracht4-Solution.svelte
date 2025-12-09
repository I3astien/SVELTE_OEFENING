<!--
FEEDBACK FOR BAS:

What he did well:
- {#each} loop works correctly
- Input binding with bind:value works perfectly
- Good validation check (if (!newTodo) return)
- Clears input after adding
- Fixed reactivity issue after guidance (used spread operator)

What he did wrong:
- Initially used todos.push() which doesn't trigger reactivity in Svelte
- Missing total count display
- Missing challenge requirement (singular/plural text with ternary)
- Didn't read all requirements before coding (again)

Concepts he struggled with:
- Svelte's reactivity rules (assignment vs mutation)
- Understanding that array methods don't trigger updates
- Using ternary operators in templates (still needs reinforcement)
- Reading complete requirements

What needs reinforcement in future assignments:
- Svelte reactivity: always reassign arrays/objects for updates
- Ternary operators in templates (keep practicing!)
- Read ALL requirements including challenge sections before starting
-->

<script>
  let todos = ['Buy groceries', 'Learn Svelte', 'Walk the dog']
  let newTodo = ''

  function addTodo() {
    if (!newTodo) return
    todos = [...todos, newTodo]
    newTodo = ''
  }
</script>

<div class="container">
  <h2>Your Todos ({todos.length})</h2>

  <ul>
    {#each todos as todo}
      <li>{todo}</li>
    {/each}
  </ul>

  <div class="input-wrapper">
    <input type="text" bind:value={newTodo} placeholder="Enter a new todo..." />
    <button on:click={addTodo}>Add</button>
  </div>

  <p class="count">
    You have {todos.length === 1 ? '1 todo' : `${todos.length} todos`}
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
  }

  ul {
    list-style: none;
    padding: 0;
    margin-bottom: 1.5rem;

    li {
      color: white;
      padding: 0.5rem;
      margin-bottom: 0.5rem;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 4px;

      &:before {
        content: '• ';
        margin-right: 0.5rem;
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
