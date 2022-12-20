<script lang="ts">
  import { currentUser, pb } from './pocketbase';

  let username: string;
  let password: string;
  let errMessage: string;

  async function login() {
    await pb.collection('users').authWithPassword(username, password);
  }

  async function signUp() {
    try {
      const data = {
        username,
        password,
        passwordConfirm: password,
        name: 'hi mom!',
      };
      const createdUser = await pb.collection('users').create(data);
      await login();
    } catch (err) {
      console.error(err.data)
      errMessage = err.data.message
      if (errMessage != '' || errMessage != undefined) {
        let errUser = err.data.data.username?.message ?? ''
        let errPass = err.data.data.password?.message ?? ''
        errMessage = errUser == '' ? errMessage : errMessage + ' Username ' + errUser
        errMessage = errPass == '' ? errMessage : errMessage + ' Password ' + errPass
      }
    }
  }

  function signOut() {
    pb.authStore.clear();
  }

</script>

{#if $currentUser}
  <p>
    Signed in as {$currentUser.username} 
    <button on:click={signOut}>Sign Out</button>
  </p>
{:else}
  <form on:submit|preventDefault>
    {#if errMessage}
      <p style="color: lightcoral">{errMessage}</p>
    {/if}
    <input
      placeholder="Username"
      type="text"
      bind:value={username}
    />

    <input 
      placeholder="Password" 
      type="password" 
      bind:value={password} 
    />
    <button on:click={signUp}>Sign Up</button>
    <button on:click={login}>Login</button>
  </form>
{/if}
