<template>
  <div id="LandingPage">
    <SignIn @send:signin="signIn" />
  </div>
</template>

<script>
import SignIn from "@/components/SignIn.vue"

export default {
  name: 'LandingPage',
  components: {
    SignIn
  },
  data() {
    return {
      user: {},
    }
  },
  methods: {
    async signIn(user) {
      try {
        const response = await fetch('/api/login', {
          method: 'POST',
          body: JSON.stringify(user),
          headers: { 'Content-type': 'application/json; charset=UTF-8' },        
        })
        const data = await response.json()
        this.user = data
        this.$router.push({name: 'Home', params: { data: data }})
      } catch(err) {
        console.log(err)
      }

    }
  }
}
</script>

<style>
</style>