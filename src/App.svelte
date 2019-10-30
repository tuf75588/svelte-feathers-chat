<script>
  import Login from "./views/Login.svelte";
  import client from "./client";
  import Chat from "./views/Chat.svelte";
  let user;
  async function login(credentials) {
    try {
      if (!credentials) {
        user = await client.reAuthenticate();
      } else {
        user = await client.authenticate({
          strategy: "local",
          ...credentials
        });
      }
      console.log(user);
    } catch (error) {
      console.error(error);
    }
  }
  login();

  async function logout() {
    await client.logout();
    user = null;
  }
</script>

<style>

</style>

<!-- if user is logged in, show chat component, if not, show login component -->

{#if !user}
  <Login {login} />
{:else}
  <Chat {logout} />
{/if}
