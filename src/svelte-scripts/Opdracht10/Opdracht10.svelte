<!-- Parent component - import UserCard and display users here -->
<script>
  import UserCard from './UserCard.svelte'
  let users = [
    {
      name: 'Bas Westerbeek',
      age: 19,
      email: 'baswesterbeek@ziggo.nl',
      role: 'Junior Web Developer',
      isOnline: true
    },
    {
      name: 'John Doe',
      age: 28,
      email: 'john@email.com',
      role: 'Developer',
      isOnline: true
    },
    {
      name: 'Jane Smith',
      age: 34,
      email: 'jane@email.com',
      role: 'Designer',
      isOnline: false
    }
  ]
</script>

<div class="users">
  {#each users as user}
    <UserCard
      name={user.name}
      age={user.age}
      email={user.email}
      role={user.role}
      isOnline={user.isOnline}
    />
  {/each}
</div>

<style lang="scss">
</style>
