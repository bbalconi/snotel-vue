<template>
  <div class='signin-top'>
    <div class='text-wrap'>
      <p class='text'>sign in:</p>
    </div>
      <form @submit.prevent="signIn">
        <div class='input-wrapper'>
          <input class='input' v-model="user.username" type="text" placeholder="username"/> 
        </div>
        <div class='input-wrapper'>
          <input class='input' v-model="user.password" type="password" placeholder="password"/> 
        </div>
        <div class='button-wrap'>
          <button class='signin-button'>//</button>
        </div>
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

<style>
.signin-top{
  align-content: center;
  margin-top: 30vh;
  height: 40vh;
}
.text-wrap{
  position: relative;
  margin-left: auto;
  margin-right: auto;
  padding-top: 8vh;
  margin-top: 3vh;
  width: 10vw;
}
.text{
  text-align: left;
}
.input-wrapper {
  position: relative;
}
.input {
  width: 10%;
  height: 14%;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.button-wrap{
    margin-top: 1.5vh;
    height: 2vh;
    position: relative;
    width: 10.2%;
    margin-left: auto;
    margin-right: auto;
}
.signin-button {
  float: right;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-weight: bold;
  border-radius: 3px;
  color: white;
  width: 32px;
  height: 30px;
  background: #ba7284;
  font-size: 1.25em;
  border: 2px solid #ba7284;
}
</style>