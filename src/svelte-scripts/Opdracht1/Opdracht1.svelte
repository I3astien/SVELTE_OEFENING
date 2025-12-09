<script>
  let name = 'Bas'
  function nameChange() {
    if (name === 'Bas') {
      name = 'World'
    } else {
      if (name === 'World') {
        name = 'Bas'
      }
    }
  }
</script>

<div class="Name">
  <div class="Name__text"><p>Hello {name}</p></div>
  <div class="Name__button">
    <button on:click={nameChange}>Change Text!</button>
  </div>
</div>

<style lang="scss">
  .Name {
    &__text {
      color: white;
    }

    &__button {
      button {
        background-color: rgb(48, 86, 48);
        color: white;
      }
    }
  }
</style>
