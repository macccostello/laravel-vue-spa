<template>


  <div class="row no-gutters full-height">
    <div class="col setting-sidebar">
      <card class="settings-card full-height">

        <ul class="nav flex-column settings-ul-nav m-t-20">

          <!-- <li v-for="tab in tabs" :key="tab.route" class="nav-item">
            <router-link :to="{ name: tab.route }" class="nav-link" active-class="active">
              <fa :icon="tab.icon" fixed-width />
              {{ tab.name }}
            </router-link>
          </li> -->

            <li class="nav-item">
                <a class="nav-link active" data-toggle="collapse" href="#collapseExample" role="button" aria-expanded="false" aria-controls="collapseExample"><span>General</span> <i class='bx bx-chevron-down bx-rotate-270' ></i></a>
                  <div class="collapse m-t-5" id="collapseExample">
                    <ul class="nav flex-column settings-ul-nav-subnav ">
                        <li class="nav-item">
                          <router-link to="profile" class="nav-link" active-class="active-tab"> Account Settings </router-link>
                        </li>

                        <li class="nav-item">
                             <router-link to="users" class="nav-link" active-class="active-tab"> Users</router-link>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#">Roles</a>
                        </li>
                          <li class="nav-item">
                            <a class="nav-link" href="#">Permissions</a>
                        </li>
                         <li class="nav-item">
                           <router-link to="password" class="nav-link" active-class="active-tab"> Change Password </router-link>
                        </li>

                    </ul>
                  </div>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Plans & Billing</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Data Center</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Integrations</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Email Settings</a>
            </li>


        </ul>


        <!-- <ul class="nav flex-column nav-pills">
          <li v-for="tab in tabs" :key="tab.route" class="nav-item">
            <router-link :to="{ name: tab.route }" class="nav-link" active-class="active">
              <fa :icon="tab.icon" fixed-width />
              {{ tab.name }}
            </router-link>
          </li>
        </ul> -->
      </card>
    </div>

    <div class="col">
      <div class="padding-30">
      <transition name="fade" mode="out-in">
        <router-view />
      </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  middleware: 'auth',

  computed: {
    // tabs () {
    //   return [
    //     {
    //       name: 'General',
    //       route: 'settings.profile'
    //     },
    //     {
    //       name: 'Plans & Billing',
    //       route: 'settings.password'
    //     },
    //     {
    //       name: 'Data Customization',
    //       route: 'settings.password'
    //     },
    //     {
    //       name: 'Integrations',
    //       route: 'settings.password'
    //     },
    //     {
    //       name: 'Email Settings',
    //       route: 'settings.password'
    //     }
    //   ]
    // },

  }
}
</script>


