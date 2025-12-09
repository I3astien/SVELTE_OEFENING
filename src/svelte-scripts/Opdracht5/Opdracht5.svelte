<script>
  let todos = []
  let newTodo = ''
  let totalTodoItems = 0

  function addTodo() {
    if (!newTodo) return
    todos = [...todos, newTodo]
    newTodo = ''
    totalTodoItems++
  }

  function remove(index) {
    todos = todos.filter((_, i) => i !== index)
    totalTodoItems--
  }
</script>

<p>Your todos ({totalTodoItems})</p>

<ol>
  {#each todos as todo, index}
    <li>
      <div class="list-children">
        <p>{todo}</p>
        <button on:click={() => remove(index)}>X</button>
      </div>
    </li>
  {/each}
</ol>

<div class="wrapper">
  <input type="text" bind:value={newTodo} />
  <button on:click={addTodo}>Add to your todo list!</button>
</div>

{#if totalTodoItems === 0}
  <p>No todos yet! Add one above!</p>
{:else}
  <p>You have {totalTodoItems} todos</p>
{/if}

<style lang="scss">
  ol {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;

    .list-children {
      display: flex;
      gap: 10rem;
    }
  }

  .wrapper {
    display: flex;
    justify-content: center;
    gap: 2rem;
  }
</style>
