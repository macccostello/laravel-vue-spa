<template>

 <div class="container-fluid p-0 m-0 full-height public-container">
      <div class="card">
                <div class="card-body">
                 <img src="images/velox-icon.svg" alt="">
                 <h1>Sign Up</h1>
                  <h2>Get started for free</h2>

                  <form @submit.prevent="register" @keydown="form.onKeydown($event)">
                    <!-- Name -->
                    <div class="form-group">
                      <label class="label">{{ $t('name') }}</label>
                        <input v-model="form.name" :class="{ 'is-invalid': form.errors.has('name') }" class="form-control public-form-control" placeholder="John Deo" type="text" name="name">
                        <has-error :form="form" field="name" />
                    </div>

                    <!-- Email -->
                    <div class="form-group">
                      <label class="label ">{{ $t('email') }}</label>

                        <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control public-form-control" placeholder="john@example.com" type="email" name="email">
                        <has-error :form="form" field="email" />

                    </div>

                    <!-- Password -->
                    <div class="form-group">
                      <label class="label ">{{ $t('password') }}</label>
                        <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" class="form-control public-form-control" placeholder="Your secret" type="password" name="password">
                        <has-error :form="form" field="password" />
                    </div>

                    <!-- Password Confirmation -->
                    <div class="form-group">
                      <label class="label ">{{ $t('confirm_password') }}</label>

                        <input v-model="form.password_confirmation" :class="{ 'is-invalid': form.errors.has('password_confirmation') }" placeholder="Confirm your secret" class="form-control public-form-control" type="password" name="password_confirmation">
                        <has-error :form="form" field="password_confirmation" />

                    </div>

                     <div  class="d-md-flex d-lg-flex align-baseline mb-3">
                         <v-button :loading="form.busy" publicButton block type="primary"> {{ $t('Sign Up') }}</v-button>
                      </div>
                        <div  class="d-md-flex d-lg-flex align-baseline ">
                        <login-with-github  />
                      </div>
                      <p class="mt-20">Already have an account?
                        <router-link :to="{ name: 'login' }"  active-class="active">
                          {{ $t('Log in now') }}
                        </router-link>
                      </p>
                  </form>
                </div>
              </div>
    </div>


</template>

<script>
import Form from 'vform'
import LoginWithGithub from '~/components/LoginWithGithub'

export default {
   layout: 'public',
  middleware: 'guest',

  components: {
    LoginWithGithub
  },

  metaInfo () {
    return { title: this.$t('register') }
  },

  data: () => ({
    form: new Form({
      name: '',
      email: '',
      password: '',
      password_confirmation: ''
    }),
    mustVerifyEmail: false
  }),

  methods: {
    async register () {
      // Register the user.
      const { data } = await this.form.post('/api/register')

      // Must verify email fist.
      if (data.status) {
        this.mustVerifyEmail = true
      } else {
        // Log in the user.
        const { data: { token } } = await this.form.post('/api/login')

        // Save the token.
        this.$store.dispatch('auth/saveToken', { token })

        // Update the user.
        await this.$store.dispatch('auth/updateUser', { user: data })

        // Redirect home.
        this.$router.push({ name: 'home' })
      }
    }
  }
}
</script>
