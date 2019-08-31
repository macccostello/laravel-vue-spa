<template>
  <nav class="navbar topbar fixed-top navbar-expand-lg navbar-light bg-white">
   <a class="navbar-brand" href="#" @click.prevent="toggleLayout"><i class='bx bx-menu'></i></a>
  <button class="navbar-toggler"  type="button" >
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarText">
    <div></div>
      <ul class="navbar-nav ml-auto">

          <li v-if="user" class="nav-item dropdown">
            <a class="nav-link dropdown-toggle text-dark avatar-text"
               href="#" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              <img :src="user.photo_url" class="rounded-circle profile-photo mr-1">
              <!-- {{ user.name }} -->
            </a>
            <div class="dropdown-menu dropdown-menu-right avatar-dropdown">
              <div class="avatar-info">
                  <p class="name">{{ user.name }}</p>
                  <p class="email">{{ user.email }}</p>
              </div>
              <router-link :to="{ name: 'settings.profile' }" class="dropdown-item mt-6">
                Profile
              </router-link>
                <router-link :to="{ name: 'settings.profile' }" class="dropdown-item ">
                Account Settings
              </router-link>

              <div class="dropdown-divider" />
              <a href="#" class="dropdown-item " @click.prevent="logout">
                {{ $t('logout') }}
              </a>
            </div>
          </li>

          <template v-else>
            <li class="nav-item">
              <router-link :to="{ name: 'login' }" class="nav-link" active-class="active">
                {{ $t('login') }}
              </router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'register' }" class="nav-link" active-class="active">
                {{ $t('register') }}
              </router-link>
            </li>
          </template>
        </ul>
  </div>
  </nav>
</template>
<script>
import { mapGetters } from 'vuex'


export default {
  name: 'Topbar',

  computed: mapGetters({
    user: 'auth/user'
  }),

  methods: {
    async logout () {
      // Log out the user.
      await this.$store.dispatch('auth/logout')

      // Redirect to login.
      this.$router.push({ name: 'login' })
    },

    toggleLayout: function(){
      var Sidebar = document.getElementById("sidebar");
      var Main = document.getElementById("main");

      Sidebar.classList.toggle("sidebar-mini");
      Main.classList.toggle("main-65");
    }
  }
}
</script>
<style scoped>
.profile-photo {
    width: 2.2rem;
    height: 2.2rem;
    /* margin: -.375rem 0; */
    object-fit: cover;
}
.avatar-text{
      font-weight: 500;
    font-size: 13px;
}
</style>
