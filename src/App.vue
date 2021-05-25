<template>
  <Navbar />
  <router-view />
</template>


<script>
  import Navbar from './components/Navbar.vue'

  export default {
    components: { Navbar }
  }
</script>

<style>
body {
  background: #f7f7f7;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  color: #555;
}
</style>
