<template>
  <Nav></Nav>
  <router-view></router-view>
</template>

<script>
import Nav from './components/Nav.vue'

export default {
  components: {
    Nav
  },

  watch: {
        $route: {
            immediate: true,
            handler(to, from) {
                document.title = to.meta.title || 'Project';
            }
        },
    },

  created() {
    sessionStorage.setItem('loggedIn', 'false');
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  height: 100vh;
  width: 100%;
}
</style>
