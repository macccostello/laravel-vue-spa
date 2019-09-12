<template>
<div class="card  card-70">
  <div class="card-header">Change Password</div>
  <div class="card-body">
    <form @submit.prevent="update" @keydown="form.onKeydown($event)">
       <alert-success :form="form" :message="'Password Updated Successfully'" />
      <div class="form-group">
        <label for="exampleInputEmail1">New Password</label>
        <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" class="form-control" type="password" name="password">
        <has-error :form="form" field="password" />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Confirm Password</label>
        <input v-model="form.password_confirmation" :class="{ 'is-invalid': form.errors.has('password_confirmation') }" class="form-control" type="password" name="password_confirmation">
        <has-error :form="form" field="password_confirmation" />
      </div>
     <v-button :loading="form.busy" type="success"> {{ $t('update') }}</v-button>
    </form>
  </div>
</div>
</template>

<script>
import Form from 'vform'

export default {
  scrollToTop: false,

  data: () => ({
    form: new Form({
      password: '',
      password_confirmation: ''
    })
  }),

  methods: {
    async update () {
      await this.form.patch('/api/settings/password')
      this.form.reset()
    }
  }
}
</script>
