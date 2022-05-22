<script>
  let email
  let confirmEmail
  let password
  let confirmPassword
  let showPassword = false
  $: type = showPassword ? 'text' : 'password'

  const handlePasswordInput = e => {
    password = e.target.value
  }
  const handleConfirmPasswordInput = e => {
    confirmPassword = e.target.value
  }

  const emailsAreEqual = data => {
    return data.email === data.confirmEmail
  }

  const passwordsAreEqual = data => {
    return data.password === data.confirmPassword
  }

  const handleSubmit = e => {
    const formData = new FormData(e.target)
    console.log('formData', formData)
    const data = {}
    for (let field of formData) {
      const [key, value] = field
      data[key] = value
    }
    if (!emailsAreEqual(data)) {
      alert('Emails do not match')
    }
    if (!passwordsAreEqual(data)) {
      alert('Passwords do not match')
    }
    console.log(data)
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
      <input type="email" name="email" id="email" placeholder="Email address" required bind:value={email} />
    </label>
    <label>
      Confirm email address
      <input type="email" name="confirmEmail" placeholder="Confirm email address" required bind:value={confirmEmail} />
    </label>
    <label>
      Password (at least 8 caracteres)
      <input {type} name="password" minlength="8" placeholder="Password" required on:input={handlePasswordInput} />
    </label>
    <label>
      Confirm Password
      <input
        {type}
        name="confirmPassword"
        placeholder="Confirm Password"
        required
        on:input={handleConfirmPasswordInput}
      />
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
