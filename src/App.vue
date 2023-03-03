<template>
  <NavBar></NavBar>
   <!-- <nav>
   <router-link to="/">Home</router-link> |
   <router-link to="/about">About</router-link>
 </nav> -->

  <router-view/>
</template>
<script>
import NavBar from './components/NavBar'
export default {
  components: { NavBar },
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #2c3e50;
}

</style>
