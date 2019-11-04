<template>
  <div class="container mt-5">
    <h3>Sign up form</h3>
    <form class="login" @submit.prevent="login">
      <h1>Sign UP</h1>
      <label>User name</label>
      <input required v-model="username" type="text" placeholder="Snoopy"/>
      <label>Password</label>
      <input required v-model="password" type="password" placeholder="Password"/>
      <hr/>
      <button type="submit" @click="createUser">Login</button>
    </form>
  </div>
</template>


<script>
  export default {
    data() {
      return {
        username: 'your email',
        password: ''
      }
    },
    methods: {
      createUser() {
        const UserEndpoint = 'http://localhost:3000/api/v1/users'
        console.log(this.username);
        console.log(this.password);
        this.$http.post(UserEndpoint, {
          email: this.username,
          password: this.password
        });
      }

    }
  }
</script>


<style>
</style>
