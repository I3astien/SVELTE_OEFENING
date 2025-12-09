<script>
  let todos = []
  let InputValue = ''
  let empty = false

  $: todoCounter = todos.length

  function addTodo() {
    if (!InputValue) {
      empty = true
      return
    } else {
      empty = false
    }
    todos = [...todos, InputValue]
    InputValue = ''
  }

  function remove(index) {
    todos = todos.filter((_, i) => i !== index)
  }
</script>

<div class="input-wrapper">
  <input
    type="text"
    bind:value={InputValue}
    placeholder="Type your todo here!"
  />
</div>
<div class="button-wrapper">
  <button on:click={addTodo}>Add todo</button>
</div>
<div class="list-wrapper">
  <ol>
    {#each todos as todo, index}
      <li>{todo}</li>
      <button on:click={() => remove(index)}>Remove</button>
    {/each}
  </ol>
</div>
{#if empty === true}
  <div class="error-wrapper">
    <p>Vul het veld in!</p>
  </div>
{/if}
{#if todoCounter > 0}
  <p>Je hebt {todoCounter} todos!</p>
{:else if todoCounter === 0}
  <p>Je hebt nog geen todos!</p>
{/if}

<style lang="scss">
  .input-wrapper {
    padding: 1rem;

    input {
      padding: 0.5rem;
    }
  }
</style>
