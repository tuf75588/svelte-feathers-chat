<script>
  export let logout;
  import client from "../client";
  let users = [];
  async function setup() {
    const { data } = await client.service("users").find();
    users = data;
  }
  setup();
</script>

<style>
  main {
    display: flex;
  }
  .user-list {
    flex: 1;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    height: 100%;
    border-right: 1px solid black;
  }
  .user-count {
    font-weight: bold;
    font-size: 2rem;
    margin-right: 0.75em;
  }

  .user {
    display: flex;
    align-items: center;
  }
  .user img {
    width: 25px;
    height: 25px;
    margin-right: 0.5rem;
    border-radius: 50%;
  }

  .user span {
    padding-left: 5px;
  }
  .user-list button {
    margin-top: 1rem;
  }
  .message-list {
    flex: 4;
  }
</style>

<main>
  <aside class="user-list">
    <span class="user-count">
      {users.length}
      <span>users</span>
    </span>
    <div class="users">
      {#each users as user}
        <div class="user">
          {#if user.avatar}
            <img src={user.avatar} alt={user.email} />
          {/if}
          <p>{user.email}</p>
        </div>
      {/each}
    </div>
    <button on:click={logout}>Logout</button>
  </aside>
  <div class="message-list">Hello</div>
  <pre>{JSON.stringify(users, null, 2)}</pre>
</main>
