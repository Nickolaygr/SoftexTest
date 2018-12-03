<template>
  <div id="app">
    <b-navbar toggleable="md" type="dark" variant="dark" class="fixed-top">
      <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
      <b-navbar-brand>
        <router-link to="/" class="navbar-brand">VueJS</router-link>
      </b-navbar-brand>
      <b-collapse is-nav id="nav_collapse">
        <b-navbar-nav>
          <b-nav-item>
            <router-link class="nav-link" to="/">Home</router-link>
          </b-nav-item>
          <b-nav-item>
            <router-link class="nav-link" to="/about">About Us</router-link>
          </b-nav-item>
          <b-nav-item>
            <router-link class="nav-link" to="/contact">Contact Us</router-link>
          </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <div class="container" style="min-height:2000px;">
      <transition name="moveInUp">
        <router-view/>
      </transition>
    </div>
  </div>
</template>
<script>
export default {
  name: 'App'
}
</script>
<style>
h1 {
  text-align: center;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.moveInUp-enter-active{
  animation: fadeIn 2s ease-in;
}
@keyframes fadeIn{
  0%{
    opacity: 0;
  }
  50%{
    opacity: 0.5;
  }
  100%{
    opacity: 1;
  }
}
.moveInUp-leave-active{
  animation: moveInUp .3s ease-in;
}
@keyframes moveInUp{
  0%{
    transform: translateY(0);
  }
  100%{
    transform: translateY(-400px);
  }
}
.navbar-dark .navbar-nav .nav-link.router-link-exact-active {
  color: rgba(255,255,255,1);
}
</style>
