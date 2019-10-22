<template>

    <div class="container-fluid p-0 m-0 full-height public-container">
      <div class="card">
                <div class="card-body">
                 <img src="images/velox-icon.svg" alt="">
                 <h1>Log In</h1>
                  <h2>Welcome back, good to see you again!</h2>
                  <form @submit.prevent="login" @keydown="form.onKeydown($event)">
                      <div class="form-group">
                        <label for="exampleInputEmail1">{{ $t('email') }}</label>
                        <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control public-form-control" type="email" name="email" placeholder="john@example.com">
                          <has-error :form="form" field="email" />
                      </div>
                      <div class="form-group">
                        <label for="exampleInputPassword1">{{ $t('password') }}</label>
                        <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" class="form-control public-form-control" type="password" name="password" placeholder="+6 Characters">
                        <has-error :form="form" field="password" />
                      </div>
                      <div class="form-group d-flex align-items-center justify-content-between">
                        <checkbox v-model="remember" name="remember">
                          {{ $t('remember_me') }}
                        </checkbox>
                           <router-link :to="{ name: 'password.request' }"  active-class="active">
                          {{ $t('Forgot your password?') }}
                        </router-link>
                      </div>
                      <div  class="d-md-flex d-lg-flex align-baseline mb-3">
                         <v-button :loading="form.busy" publicButton block type="primary"> {{ $t('Login') }}</v-button>
                      </div>
                        <div  class="d-md-flex d-lg-flex align-baseline ">
                        <login-with-github  />
                      </div>


                      <p class="mt-20">Don't have an account?
                        <router-link :to="{ name: 'register' }"  active-class="active">
                          {{ $t('Sign up now') }}
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



  data: () => ({
    form: new Form({
      email: '',
      password: ''
    }),
    remember: false
  }),

  methods: {
    async login () {
      // Submit the form.
      const { data } = await this.form.post('/api/login')

      // Save the token.
      this.$store.dispatch('auth/saveToken', {
        token: data.token,
        remember: this.remember
      })

      // Fetch the user.
      await this.$store.dispatch('auth/fetchUser')

      // Redirect home.
      this.$router.push({ name: 'home' })
    }
  }
}
</script>
