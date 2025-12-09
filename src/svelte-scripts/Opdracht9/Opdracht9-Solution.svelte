<!--
FEEDBACK FOR BAS:

What he did right:
- NAILED the edit state management with editingIndex and editValue!
- Conditional rendering inside the loop works correctly
- All three edit functions implemented properly
- UI switches correctly between view/edit modes
- Still using immutable array updates correctly
- Clean code structure

What he did wrong:
- Missing validation: Save button should be disabled when editValue is empty
- Still not using .trim() in addTodo validation (feedback from Opdracht 8)
- No empty state message ("No todos yet!" when list is empty)
- Typo: "eem" should be "een"

Concepts he struggled with:
- Applying previous feedback (.trim() validation)
- Using reactive statements for button disabled state
- Empty state handling

What needs reinforcement in future assignments:
- Read and apply previous feedback
- Use .trim() consistently for text validation
- Reactive statements for derived UI state (like button disabled)
- Empty state handling
-->

<script>
  let todos = []
  let inputValue = ''

  // Editing state
  let editingIndex = null
  let editValue = ''

  // Reactive validation
  $: canSave = editValue.trim() !== ''
  $: canAdd = inputValue.trim() !== ''

  function addTodo() {
    if (inputValue.trim() !== '') {
      todos = [...todos, inputValue.trim()]
      inputValue = ''
    }
  }

  function remove(index) {
    todos = todos.filter((_, i) => i !== index)
  }

  function startEdit(index) {
    editingIndex = index
    editValue = todos[index]
  }

  function saveEdit() {
    if (editValue.trim() !== '') {
      todos[editingIndex] = editValue.trim()
      todos = todos  // Trigger reactivity
      editingIndex = null
      editValue = ''
    }
  }

  function cancelEdit() {
    editingIndex = null
    editValue = ''
  }
</script>

<div class="todo-app">
  <h2>My Todo List</h2>

  <div class="input-section">
    <input
      type="text"
      bind:value={inputValue}
      placeholder="Add a new todo..."
    />
    <button on:click={addTodo} disabled={!canAdd}>
      Add
    </button>
  </div>

  <div class="todo-list">
    {#if todos.length === 0}
      <p class="empty-message">No todos yet! Add one above.</p>
    {:else}
      <ul>
        {#each todos as todo, index}
          <li class="todo-item">
            {#if editingIndex === index}
              <!-- Edit mode -->
              <input
                type="text"
                class="edit-input"
                bind:value={editValue}
              />
              <div class="button-group">
                <button class="save-btn" on:click={saveEdit} disabled={!canSave}>
                  Save
                </button>
                <button class="cancel-btn" on:click={cancelEdit}>
                  Cancel
                </button>
              </div>
            {:else}
              <!-- View mode -->
              <span class="todo-text">{todo}</span>
              <div class="button-group">
                <button class="edit-btn" on:click={() => startEdit(index)}>
                  Edit
                </button>
                <button class="remove-btn" on:click={() => remove(index)}>
                  Remove
                </button>
              </div>
            {/if}
          </li>
        {/each}
      </ul>
    {/if}
  </div>
</div>

<style lang="scss">
  .todo-app {
    max-width: 600px;
    margin: 2rem auto;
    padding: 2rem;
    background: #f5f5f5;
    border-radius: 8px;

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

    ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }
  }

  .todo-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0.75rem;
    margin-bottom: 0.5rem;
    background: white;
    border-radius: 4px;
    border: 1px solid #e0e0e0;

    .todo-text {
      flex: 1;
      color: #333;
    }

    .edit-input {
      flex: 1;
      padding: 0.5rem;
      border: 2px solid #4CAF50;
      border-radius: 4px;
      font-size: 1rem;

      &:focus {
        outline: none;
        border-color: #45a049;
      }
    }

    .button-group {
      display: flex;
      gap: 0.5rem;
      margin-left: 1rem;
    }

    button {
      padding: 0.4rem 0.8rem;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.9rem;
      font-weight: 500;

      &:disabled {
        opacity: 0.5;
        cursor: not-allowed;
      }
    }

    .edit-btn {
      background: #2196F3;
      color: white;

      &:hover {
        background: #1976D2;
      }
    }

    .remove-btn {
      background: #f44336;
      color: white;

      &:hover {
        background: #d32f2f;
      }
    }

    .save-btn {
      background: #4CAF50;
      color: white;

      &:hover:not(:disabled) {
        background: #45a049;
      }
    }

    .cancel-btn {
      background: #757575;
      color: white;

      &:hover {
        background: #616161;
      }
    }
  }
</style>
