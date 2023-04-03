<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Register!</h2>

          {{ JSON.stringify($axios) }}
          <Notification v-if="error" :message="error" />

          <form method="post" @submit.prevent="register">
            <div class="field">
              <label class="label" for="display_name">Username</label>
              <div class="control">
                <input
                  id="display_name"
                  v-model="display_name"
                  type="text"
                  class="input"
                  name="display_name"
                  required
                />
              </div>
            </div>
            <div class="field">
              <label class="label" for="email">Email</label>
              <div class="control">
                <input
                  id="email"
                  v-model="email"
                  type="email"
                  class="input"
                  name="email"
                  required
                />
              </div>
            </div>
            <div class="field">
              <label class="label" for="password">Password</label>
              <div class="control">
                <input
                  id="password"
                  v-model="password"
                  type="password"
                  class="input"
                  name="password"
                  required
                />
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">
                Register
              </button>
            </div>
          </form>

          <div class="has-text-centered" style="margin-top: 20px">
            Already got an account? <nuxt-link to="/login">Login</nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Auth/Notification'

export default {
  components: {
    Notification
  },
  layout: 'auth',
  middleware: 'guest',

  data() {
    return {
      display_name: '',
      email: '',
      password: '',
      error: null
    }
  },

  methods: {
    async register() {
      try {
        await this.$axios.post('/api/register', {
          display_name: this.display_name,
          email: this.email,
          password: this.password
        })

        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/')
      } catch (e) {
        this.error = e.response.data.message
      }
    }
  }
}
</script>
