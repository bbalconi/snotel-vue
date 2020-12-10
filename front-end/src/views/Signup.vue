<template>
  <div>
    <form @submit.prevent="signUp">
      <input v-model="user.username" type="text" placeholder="username"/> 
      <input v-model="user.password" type="password" placeholder="password"/> 
      <input v-model="user.confirmPassword" type="password" placeholder="confirm password"/> 
      <button>Sign Up</button>
    </form>
    <p v-if="error">Please check values and try again!</p>
  </div>
</template>

<script>
export default {
  name: 'sign-in',
  data() {
    return {
      error: false,
      user: {
        username: '',
        password: '',
        confirmPassword: ''
      }
    }
  },
  methods: {
    async signUp() {
      if (this.user.password !== this.user.confirmPassword) {
        this.error = true
      } else {
          await fetch('/api/saveUser', {
            method: 'POST',
            body: JSON.stringify({username:this.user.username,password:this.user.password}),
            headers: { 'Content-type': 'application/json; charset=UTF-8' },        
          })
            this.$router.push({name: 'LandingPage'})
      }
    }
  }
}
</script>