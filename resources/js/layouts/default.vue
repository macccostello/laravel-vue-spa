<template>
  <div class="main-layout full-height">
    <Sidebar />
    <main  id="main" class="full-height">
    <Topbar  />
    <div class="content-area full-height">
      <child />
    </div>
</main>
  </div>
</template>

<script>
import Topbar from '~/components/Topbar'
import Sidebar from '~/components/Sidebar'

export default {
  name: 'MainLayout',
  components: {
    Topbar,
    Sidebar
  }
}
</script>
