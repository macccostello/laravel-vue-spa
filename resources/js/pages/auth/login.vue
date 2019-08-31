<template>

    <div class="container-fluid p-0 m-0 full-height">
      <div class="row no-gutters full-height">
        <div class="col-lg-4  full-height left-side d-none d-sm-none d-md-none  d-lg-block">
          <svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
            viewBox="0 0 512 512" style="enable-background:new 0 0 512 512; width:17%;" xml:space="preserve">
              <g>
                <g>
                  <path fill="#c3ef6c" d="M362.667,68.188V10.667C362.667,4.771,357.896,0,352,0h-64c-4.104,0-7.854,2.354-9.625,6.063l-17.479,36.552
                    c-0.406,0-0.823,0.01-1.219,0.01L256,42.667c-129.396,0-234.667,105.271-234.667,234.667c0,40.083,10.417,79.792,30.115,114.833
                    c1.948,3.458,5.74,5.531,9.656,5.427c3.979-0.125,7.552-2.458,9.271-6.052l24.042-50.271c1.208-2.531,1.375-5.448,0.458-8.094
                    c-6.333-18.271-9.542-37.063-9.542-55.844c0-84.802,61.906-155.656,144-168.708L43.708,496.729
                    c-1.583,3.302-1.354,7.188,0.604,10.292c1.948,3.104,5.354,4.979,9.021,4.979h64c4.271,0,8.125-2.542,9.802-6.469l61.229-142.865
                    H288v10.667c0,4.104,2.354,7.833,6.042,9.615c3.708,1.792,8.083,1.271,11.292-1.281L358.667,339c2.531-2.031,4-5.094,4-8.333
                    c0-3.24-1.469-6.302-4-8.333l-53.333-42.667c-3.219-2.573-7.625-3.083-11.292-1.281c-3.688,1.781-6.042,5.51-6.042,9.615v10.667
                    h-68.833L288,145.698v99.635c0,3.24,1.469,6.302,4,8.333l53.333,42.667c3.188,2.563,7.594,3.052,11.292,1.281
                    c3.688-1.781,6.042-5.51,6.042-9.615V144.417c40.406,32.417,64,80.802,64,132.917c0,53.753-25.039,101.707-64,133.014v-37.014
                    c0-4.104-2.354-7.833-6.042-9.615c-3.708-1.781-8.094-1.281-11.292,1.281L292,407.667c-3.531,2.833-4.896,7.594-3.396,11.865
                    c1.5,4.271,5.531,7.135,10.063,7.135h39.773C313.98,440.225,285.892,448,256,448c-22.042,0-43.646-4.24-64.208-12.604
                    c-5.375-2.146-11.531,0.344-13.823,5.688l-16.813,39.24c-1.125,2.625-1.156,5.594-0.073,8.229c1.083,2.646,3.177,4.75,5.823,5.833
                    C195.333,506.073,225.313,512,256,512c129.396,0,234.667-105.271,234.667-234.667C490.667,189.708,440.646,108.354,362.667,68.188
                    z"/>
                </g>
              </g>
          </svg>
          <h1>Your Space <br> To Be Social.</h1>
          <h5>Blast off today and join the fun! Getting started is <br> only a few clicks away</h5>
          <!-- <div class="public-svg">
            <svg xmlns="http://www.w3.org/2000/svg" class="db h-100p w-100p" enable-background="new 0 0 475 475" height="475" id="svg-25e6tnbe4ecg" viewBox="0 0 475 475" width="475"><path d="m78 140.8-70-70 70-70 70 70z" fill="#54cd52"></path><path d="m78 100.5-29.7-29.8 29.7-29.7 29.7 29.7z" fill="#2d216d"></path><g transform="matrix(-.70710678 -.70710678 .70710678 -.70710678 236.26 576.36)"><path d="m71.3 73.1h332.3v332.3h-332.3z" fill="#917cf7"></path><path d="m167 168.7h141v141.1h-141z" fill="#2d216d"></path></g></svg>
          </div> -->
        </div>
        <div class="col-lg-8 col-md-12 col-sm-12 full-height">
            <div class="right-side full-height">
              <div class="card">
                <div class="card-body">
                  <h2>Welcome back, good to see you again!</h2>
                  <form @submit.prevent="login" @keydown="form.onKeydown($event)">
                      <div class="form-group">
                        <label for="exampleInputEmail1">{{ $t('email') }}</label>
                        <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control public-form-control" type="email" name="email">
                          <has-error :form="form" field="email" />
                      </div>
                      <div class="form-group">
                        <label for="exampleInputPassword1">{{ $t('password') }}</label>
                        <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" class="form-control public-form-control" type="password" name="password">
                        <has-error :form="form" field="password" />
                      </div>
                      <div class="form-group d-flex align-items-center justify-content-between">
                        <checkbox v-model="remember" name="remember">
                          {{ $t('remember_me') }}
                        </checkbox>
                          <a href="">Forgot your password?</a>
                      </div>
                      <div  class="d-md-flex d-lg-flex align-baseline ">
                        <button type="submit" class="btn btn-primary btn-block btn-public mr-20 mb-10" :loading="form.busy">{{ $t('login') }}</button>
                        <login-with-github />
                          <!-- <button type="submit" class="btn btn-primary btn-block btn-public mr-20 mb-10">Log In</button> -->
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
