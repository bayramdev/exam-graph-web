<template>
  <div>
    <form @submit.prevent="userLogin">
      <div>
        <label>Username</label>
        <input type="text" v-model="login.userID" />
      </div>
      <div>
        <label>Password</label>
        <input type="password" v-model="login.userPassword" />
      </div>
      <div>
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      login: {
        userID: '',
        userPassword: '',
      },
    }
  },

  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith('local', { data: this.login })
        console.log('LOGIN RESPONSE:', response)
        console.log('LOGGED IN AS USER:', this.$auth.user)
      } catch (err) {
        console.error(err)
      }
    },
  },
}
</script>