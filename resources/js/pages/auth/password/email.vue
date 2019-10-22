<template>
 <div class="container-fluid p-0 m-0 full-height public-container">
      <div class="card">
                <div class="card-body">
                 <img src="images/velox-icon.svg" alt="">
                  <h1>Reset Your Password</h1>
                  <h2>Check your inbox. we just sent you reset link.</h2>
                   <form @submit.prevent="send" @keydown="form.onKeydown($event)">
                      <alert-success :form="form" :message="status" />
                      <div class="form-group">
                        <label class="label">{{ $t('email') }}</label>
                          <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control public-form-control" type="email" name="email">
                          <has-error :form="form" field="email" />
                      </div>
                      <div class="form-group ">
                          <v-button :loading="form.busy" publicButton block type="primary">
                            {{ $t('send_password_reset_link') }}
                          </v-button>
                      </div>
                       <p class="mt-20">Back to
                        <router-link :to="{ name: 'login' }"  active-class="active">
                          {{ $t('Log in now') }}
                        </router-link>
                      </p>
                    </form>
                </div>
        </div>
  </div>


  <!-- <div class="row">
    <div class="col-lg-8 m-auto">
      <card :title="$t('reset_password')">
        <form @submit.prevent="send" @keydown="form.onKeydown($event)">
          <alert-success :form="form" :message="status" />


          <div class="form-group row">
            <label class="col-md-3 col-form-label text-md-right">{{ $t('email') }}</label>
            <div class="col-md-7">
              <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control" type="email" name="email">
              <has-error :form="form" field="email" />
            </div>
          </div>

          <div class="form-group row">
            <div class="col-md-9 ml-md-auto">
              <v-button :loading="form.busy">
                {{ $t('send_password_reset_link') }}
              </v-button>
            </div>
          </div>
        </form>
      </card>
    </div>
  </div> -->
</template>

<script>
import Form from 'vform'

export default {
  layout: 'public',
  middleware: 'guest',

  metaInfo () {
    return { title: this.$t('reset_password') }
  },

  data: () => ({
    status: '',
    form: new Form({
      email: ''
    })
  }),

  methods: {
    async send () {
      const { data } = await this.form.post('/api/password/email')

      this.status = data.status

      this.form.reset()
    }
  }
}
</script>
