<script>
  export let logout;
  import client from "../client";
  let users = [];
  let messages = [];
  async function setup() {
    ({ data: users } = await client.service("users").find());
    ({ data: messages } = await client.service("messages").find());
    console.log(messages);
  }
  setup();
</script>

<style>
  main {
    display: flex;
    height: 97.5%;
    position: relative;
  }
  .user-list {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    height: 100%;
    border-right: 1px solid hsl(0, 0%, 80%);
    background: hsl(0, 0%, 92%);
  }
  .users {
    flex-grow: 1;
  }
  .logout {
    width: 100%;
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
    margin-bottom: 2rem;
  }
  .message-list {
    flex: 4;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    height: 100%;
  }
  .messages {
    overflow: scroll;
    flex-grow: 1;
  }
  .message-form {
    height: 10%;
    margin: 0.3rem;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }
  .message-form input {
    width: 84%;
    margin: 30px 10px;
    box-sizing: border-box;
    padding: 0.7rem 1rem;
  }
  .message-form button {
    height: 35%;
    margin: 0;
    font-size: 1em;
    color: #fff;
    box-sizing: border-box;
    /* background-color: #0B3954; */
    background-color: #66b99e;
  }
  .user-count {
    margin-bottom: 0.5em;
  }
  .user-count-num {
    font-weight: bold;
    margin-right: 0.5rem;
  }
  .user {
    display: flex;
    align-items: center;
  }
  .user p {
    font-weight: bold;
    opacity: 0.7;
  }
  .user img {
    width: 25px;
    height: 25px;
    margin-right: 0.5rem;
    border-radius: 50%;
  }
  .message {
    padding: 0 15px 5px;
    border-radius: 10px;
    background-color: hsl(0, 0%, 100%);
  }
  .message:nth-child(odd) {
    background-color: hsl(0, 0%, 97%);
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
    <button on:click={logout} class="logout">Logout</button>
  </aside>
  <div class="message-list">
    <div class="messages">
      {#each messages as message}
        <div class="message">
          <div class="user">
            <img src={message.user.avatar} alt="user" />
            <p>{message.user.text}</p>
          </div>
        </div>
      {/each}
    </div>
    <form class="message-form">
      <input placeholder="send message" type="text" name="message" />
      <button type="button">send message</button>
    </form>

  </div>

</main>
