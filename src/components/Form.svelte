<script>
  let email
  let confirmEmail
  let password
  let confirmPassword
  let showPassword = false

  const handleSubmit = () => {
    console.log(email, confirmEmail, password, confirmPassword, showPassword)
  }
</script>

<main>
  <form class="form" on:submit|preventDefault={handleSubmit}>
    <p>Create an account</p>
    <button>Sign up with Google</button>
    <div class="orSection">
      <hr />
      or
      <hr />
    </div>
    <label>
      Email address
      <input type="email" name="email" id="email" placeholder="Email address" bind:value={email} />
    </label>
    <label>
      Confirm email address
      <input type="email" name="confirmEmail" placeholder="Confirm email address" bind:value={confirmEmail} />
    </label>
    <label>
      Password (at least 8 caracteres)
      <input type="password" name="password" placeholder="Password" bind:value={password} />
    </label>
    <label>
      Confirm Password
      <input type="password" name="confirmPassword" placeholder="Confirm Password" bind:value={confirmPassword} />
    </label>
    <label>
      <input type="checkbox" bind:checked={showPassword} />
      Show Password
    </label>
    <button>Sign Up</button>
  </form>
</main>

<style>
</style>
