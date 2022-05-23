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
    console.log('formData', formData)
    const data = {}
    for (let field of formData) {
      const [key, value] = field
      data[key] = value
    }
    console.log(data)
  }
</script>

<main class="window">
  <div class="title-bar">
    <div class="title-bar-text">Create an account</div>
  </div>
  <div class="window-body">
    <button id="google-login-btn"><img src="./Google-G-Logo.svg" id="google-logo" />Sign up with Google</button>
    <div class="orSection">or</div>
    <form on:submit|preventDefault={handleSubmit}>
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
          id="confirm-password"
          name="confirmPassword"
          placeholder="Confirm Password"
          required
          on:input={handleConfirmPasswordInput}
          on:input={validateConfirmPassword}
        />
      </div>
      <div class="field-row">
        <input id="show-pw-checkbox" type="checkbox" bind:checked={showPassword} />
        <label for="show-pw-checkbox">Show Password </label>
      </div>
      <button>Sign up</button>
    </form>
    <p class="window-footer">Already have an account? <a href="https://cohere.ai/"> Log in</a></p>
  </div>
</main>

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
