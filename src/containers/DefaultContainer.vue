<template>
  <div class="app">
    <AppHeader fixed>
      <SidebarToggler class="d-lg-none" display="md" mobile />
      <SidebarToggler class="d-md-down-none" display="lg" />
      <b-link class="navbar-brand" to="#">
        <img class="navbar-brand-full" src="img/logobright.png" width="110" height="50" >
        <img class="navbar-brand-minimized" src="img/logobright.png" width="30" height="30" alt="CoreUI Logo">
      </b-link>

      <b-navbar-nav class="ml-auto">
        <b-nav-item class="d-md-down-none">
          <p style="font-size: 20px">|</p>
        </b-nav-item>
        <b-nav-item class="d-md-down-none">
          <p style="font-size: 25px; align-content: center"> Eb Pearl </p>
        </b-nav-item>
       <DefaultHeaderDropdownAccnt/>
        <b-nav-item class="d-md-down-none">
                  <img
          src="img/avatars/6.jpg"
          class="img-avatar"
          alt="admin@bootstrapmaster.com" />
        </b-nav-item>
      </b-navbar-nav>
    </AppHeader>
    <div class="app-body">
      <AppSidebar fixed>
        <SidebarHeader/>
        <SidebarForm/>
        <SidebarNav :navItems="nav"></SidebarNav>
        <SidebarFooter/>
        <SidebarMinimizer/>
      </AppSidebar>
      <main class="main">
        <p style="font-size: 40px; padding-left: 30px"> Welcome Back</p>
        <p style="align-content: baseline" id="date"> </p>
        <div class="container-fluid">
          <router-view></router-view>
        </div>
      </main>
      </div>
  </div>
</template>

<script>
  import nav from '@/_nav'
  import { Header as AppHeader, SidebarToggler, Sidebar as AppSidebar, SidebarFooter, SidebarForm, SidebarHeader, SidebarMinimizer, SidebarNav, Aside as AppAside, AsideToggler, Footer as TheFooter, Breadcrumb } from '@coreui/vue'
  import DefaultAside from './DefaultAside'
  import DefaultHeaderDropdownAccnt from './DefaultHeaderDropdownAccnt'

  export default {
    name: 'DefaultContainer',
    components: {
      AsideToggler,
      AppHeader,
      AppSidebar,
      AppAside,
      TheFooter,
      Breadcrumb,
      DefaultAside,
      DefaultHeaderDropdownAccnt,
      SidebarForm,
      SidebarFooter,
      SidebarToggler,
      SidebarHeader,
      SidebarNav,
      SidebarMinimizer
    },
    data () {
      return {
        nav: nav.items
      }
    },
    computed: {
      name () {
        return this.$route.name
      },
      list () {
        return this.$route.matched.filter((route) => route.name || route.meta.label )
      }
    }
  }
</script>
