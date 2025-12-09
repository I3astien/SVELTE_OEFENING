<script>
  let todos = []
  let inputValue = ''

  let empty = false

  function addTodo() {
    if (!inputValue) {
      empty = true
      return
    } else empty = false

    todos = [...todos, inputValue]
    inputValue = ''
  }

  function remove(index) {
    todos = todos.filter((_, i) => i !== index)
  }

  let editingIndex = null // Which todo is being edited? (null = none)
  let editValue = '' // What's the text in the edit field?

  function startEdit(index) {
    editingIndex = index // "We're editing todo #2"
    editValue = todos[index] // Put current text in the edit field
  }

  function saveEdit() {
    todos[editingIndex] = editValue.trim() // Update the todo
    todos = todos // Trigger reactivity
    editingIndex = null // Done editing
  }

  function cancelEdit() {
    editingIndex = null // Stop editing, forget changes
  }
</script>

<div class="container">
  <div class="container__inner">
    <div class="input-wrapper">
      <input type="text" bind:value={inputValue} />
      <button on:click={addTodo}>Voeg eem todo toe!</button>
    </div>
    <div class="list-wrapper">
      {#if empty}
        <p>De input field is leeg!</p>
      {/if}
      <ul>
        {#each todos as todo, index}
          <div class="list-item-wrapper">
            {#if editingIndex === index}
              <!-- This todo is being edited - show input -->
              <input type="text" bind:value={editValue} />
              <button on:click={saveEdit}>Opslaan</button>
              <button on:click={cancelEdit}>Annuleer</button>
            {:else}
              <!-- Normal view - show text and buttons -->
              <li>{todo}</li>
              <button on:click={() => startEdit(index)}>Bewerk</button>
              <button on:click={() => remove(index)}>Verwijder</button>
            {/if}
          </div>
        {/each}
      </ul>
    </div>
  </div>
</div>

<style lang="scss">
  .container {
    border-radius: 1rem;
    background-color: rgb(84, 84, 84);

    &__inner {
      padding: 3rem;

      .input-wrapper {
        display: flex;
        justify-content: center;
        gap: 1rem;

        input {
          background-color: black;
          border-radius: 0.5rem;
          border: none;
          width: 50%;
        }

        button {
          background-color: black;
          border-radius: 0.5rem;
          border: none;
          width: 50%;
        }
      }

      .list-wrapper {
        margin-top: 1rem;
        padding: 1rem;
        background-color: black;
        color: white;
        border-radius: 1rem;

        ul {
          display: flex;
          align-items: center;
          justify-content: center;
          flex-direction: column;
          gap: 1rem;

          .list-item-wrapper {
            display: flex;
            flex-direction: row;
            align-items: center;
            gap: 10rem;
          }
        }
      }
    }
  }
</style>
