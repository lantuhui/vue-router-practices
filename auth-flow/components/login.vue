<template>
  <div>
    <h2>Login</h2>
    <p v-if="$route.query.redirect">
      You need to login first.
    </p>
    <form @submit.prevent="login">
      <label><input v-model="email" placeholder="email"></label>
      <label><input v-model="pass" placeholder="password" type="password"></label> (hint: password1)<br>
      <button type="submit">login</button>
      <p v-if="error" class="error">Bad login information</p>
    </form>
  </div>
</template>

<script type="text/javascript">
  import auth from '../auth'

  export default {
    data(){
      return {
        email:'fengmeiru@lantu.com',
        pass:'',
        error:false
      }
    },
    methods:{
      login(){
        auth.login(this.email,this.pass,loggedIn =>{
          if(!loggedIn){
            this.error = true
          }else{
            this.$router.replace(this.$route.query.redirect || '/')
          }
        })
      }
    }
  }
</script>

<style type="text/css">
  .error{
    color:red;
  }
</style>