<script>
  export let login;
  import client from "../client";

  const user = {
    email: "",
    password: ""
  };
  async function signupAndLogin() {
    await client.service("users").create(user);
    login(user);
  }

  function loginWithGithub() {
    window.location.href = "http://localhost:3030/oauth/github";
  }
</script>

<style>
  form {
    max-width: 400px;
    margin: 0 auto;
  }
  input {
    width: 100%;
  }
  button {
    display: block;
    margin: 1rem 0;
    border-radius: 5px;
    width: 100%;
  }
  h2 {
    text-align: center;
    font-weight: 400;
  }
  label div,
  label input {
    margin: 0 0 0.5rem 0;
  }
  .gh {
    background: red;
    outline: 0;
    color: #fff;
  }
</style>

<h2 class="header">Login or Sign up</h2>
<form>
  <label>
    <div>Email</div>
    <input type="email" name="email" bind:value={user.email} />
  </label>
  <label for="password">
    <div>Password</div>
    <input type="password" name="password" bind:value={user.password} />
  </label>
  <button on:click={() => login(user)} type="button">Login</button>
  <button on:click={signupAndLogin} type="button">Sign up and Login</button>
  <button class="gh" on:click={loginWithGithub} type="button">
    Login with GitHub
  </button>
</form>
