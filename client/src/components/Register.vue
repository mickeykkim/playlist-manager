<template>
  <v-layout column>
    <v-flex>
      <panel title="Register">
        <form
          name="tab-tracker-form"
          autocomplete="off">
          <v-text-field
            dark
            label="New User Email"
            v-model="email"
          ></v-text-field>
          <br>
          <v-text-field
            dark
            label="New User Password"
            type="password"
            v-model="password"
            autocomplete="new-password"
            @keyup.enter.native="login"
          ></v-text-field>
        </form>
        <br>
        <div class="danger-alert" v-html="error" />
        <br>
        <v-btn
          dark
          class="light-blue darken-1"
          @click="register">
          <v-icon dark left>check_circle</v-icon>
          Register
        </v-btn>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  watch: {
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          username: this.username,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
        this.$router.push({
          name: 'songs'
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  },
  mounted () {
  }
}
</script>

<style scoped>
</style>
