<template>

<div class="card table-card card-70">
  <div class="card-header">Account Settings </div>
  <div class="card-body">
    <form  @submit.prevent="update" @keydown="form.onKeydown($event)">
       <alert-success :form="form" :message="'Account Settings Updated Successfully'" />
      <div class="form-group">
        <label for="exampleInputEmail1">Email address</label>
        <input v-model="form.name" :class="{ 'is-invalid': form.errors.has('name') }" class="form-control" type="text" name="name">
          <has-error :form="form" field="name" />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Password</label>
         <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-control" type="email" name="email">
          <has-error :form="form" field="email" />
      </div>

     <v-button :loading="form.busy" type="success"> {{ $t('update') }}</v-button>
    </form>

  </div>
</div>


</template>

<script>
import Form from 'vform'
import { mapGetters } from 'vuex'

export default {
  scrollToTop: false,

  metaInfo () {
    return { title: this.$t('settings') }
  },

  data: () => ({
    form: new Form({
      name: '',
      email: ''
    })
  }),

  computed: mapGetters({
    user: 'auth/user'
  }),

  created () {
    // Fill the form with user data.
    this.form.keys().forEach(key => {
      this.form[key] = this.user[key]
    })
  },

  methods: {
    async update () {
      const { data } = await this.form.patch('/api/settings/profile')

      this.$store.dispatch('auth/updateUser', { user: data })
    }
  }
}
</script>
