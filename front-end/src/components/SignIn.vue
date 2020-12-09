<template>
  <div>
    <form @submit.prevent="signIn">
      <input v-model="user.username" type="text" label="username"/> 
      <input v-model="user.password" type="text" label="password"/> 
      <button>Sign In</button>
    </form>
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
    }
  }
}
</script>