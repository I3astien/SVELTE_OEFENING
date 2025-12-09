<script>
  let todos = ['Buy Groceries', 'Learn Svelte', 'Walk the dog']
  let newTodo = ''

  function addTodo() {
    if (!newTodo) return
    todos = [...todos, newTodo]
    newTodo = ''
  }
</script>

<ul>
  {#each todos as todo}
    <li>{todo}</li>
  {/each}
</ul>

<div class="wrapper">
  <input type="text" bind:value={newTodo} />
  <button on:click={addTodo}>Add to your todo list!</button>
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    justify-content: center;
    gap: 2rem;
  }
</style>
