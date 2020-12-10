<template>
  <div>
    <form @submit.prevent="signIn">
      <input v-model="user.username" type="text" placeholder="username"/> 
      <input v-model="user.password" type="password" placeholder="password"/> 
      <button>Sign In</button>
    </form>
    <a @click="signUp">sign up</a>
  </div>
</template>

<script>
export default {
  name: 'sign-in',
  data() {
    return {
      user: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    signIn() {
      this.$emit('send:signin', this.user)
    }, signUp(){
      this.$router.push({name: 'Signup'})
    }
  }
}
</script>