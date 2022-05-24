<script>
  let email
  let confirmEmail
  let password = ''
  let confirmPassword = ''
  let showPassword = false
  $: type = showPassword ? 'text' : 'password'

  const resetForm = () => {
    email = ''
    confirmEmail = ''
    password = ''
    confirmPassword = ''
  }

  const handlePasswordInput = e => {
    password = e.target.value
  }
  const handleConfirmPasswordInput = e => {
    confirmPassword = e.target.value
    validateConfirmPassword(e)
  }

  const validateConfirmEmail = e => {
    let textbox = e.target
    if (textbox.value !== email) {
      textbox.setCustomValidity('The email confirmation does not match.')
    } else {
      textbox.setCustomValidity('')
    }
    return true
  }

  const validateConfirmPassword = e => {
    let textbox = e.target
    if (textbox.value !== password) {
      textbox.setCustomValidity('The password confirmation does not match.')
    } else {
      textbox.setCustomValidity('')
    }
    return true
  }

  const handleSubmit = e => {
    const formData = new FormData(e.target)
    const data = {}
    for (let field of formData) {
      const [key, value] = field
      data[key] = value
    }
    console.log(data)
    resetForm()
  }

  const loginWithGoogle = () => {
    console.log('Sign up with Google')
  }
</script>

<div class="window">
  <div class="title-bar">
    <div class="title-bar-text">Create an account</div>
  </div>
  <div class="window-body">
    <button id="google-login-btn" on:click={loginWithGoogle}
      ><img src="./Google-G-Logo.svg" id="google-logo" alt="Google icon" />Sign up with Google</button
    >
    <div class="or-section">or</div>
    <form on:submit|preventDefault={handleSubmit} id="sign-up-form">
      <div class="field-row-stacked">
        <label for="email">Email address</label>
        <input id="email" type="email" name="email" placeholder="Email address" required bind:value={email} />
      </div>
      <div class="field-row-stacked">
        <label for="confirm-email">Confirm email address</label>
        <input
          id="confirm-email"
          type="email"
          name="confirmEmail"
          placeholder="Confirm email address"
          required
          bind:value={confirmEmail}
          on:change={validateConfirmEmail}
        />
      </div>
      <div class="field-row-stacked">
        <label for="password"> Password (at least 8 caracteres)</label>
        <input
          {type}
          value={password}
          id="password"
          name="password"
          minlength="8"
          placeholder="Password"
          required
          on:input={handlePasswordInput}
        />
      </div>
      <div class="field-row-stacked">
        <label for="confirm-password"> Confirm Password</label>
        <input
          {type}
          value={confirmPassword}
          id="confirm-password"
          name="confirmPassword"
          placeholder="Confirm Password"
          required
          on:input={handleConfirmPasswordInput}
        />
      </div>
      <div class="field-row">
        <input id="show-pw-checkbox" type="checkbox" bind:checked={showPassword} />
        <label for="show-pw-checkbox">Show Password </label>
      </div>
      <button>Sign up</button>
    </form>
    <p class="form-footer">Already have an account? <a target="_blank" href="https://cohere.ai/"> Log in</a></p>
  </div>
</div>

<style>
  #show-pw-checkbox {
    display: none;
  }

  #google-logo {
    height: 14px;
  }

  #google-login-btn {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 6px;
  }
</style>
