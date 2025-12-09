<!-- UserCard component - accepts props and displays user info -->
<script>
  export let name
  export let age
  export let email
  export let role
  export let isOnline = false // Optional prop with default value
</script>

<div class="card">
  <h3>{name}</h3>
  <p>Age: {age}</p>
  <p>{email}</p>
  <p>Role: {role}</p>
  {#if isOnline}
    <span>🟢 Online</span>
  {:else}
    <span>⚫ Offline</span>
  {/if}
</div>

<style lang="scss">
  /* Your card styles here */
</style>
