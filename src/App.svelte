<script>
  import Login from "./views/Login.svelte";
  import client from "./client";
  import Chat from "./views/Chat.svelte";
  let user;
  async function login() {
    try {
      user = await client.reAuthenticate();
    } catch (error) {
      console.error(error);
    }
  }
  login();
</script>

<style>

</style>

<!-- if user is logged in, show chat component, if not, show login component -->

{#if !user}
  <Login />
{:else}
  <Chat />
{/if}
