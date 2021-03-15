<template>
  <Navbar />
  <router-view class="container" />
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
  components: {
    Navbar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  width: 100vw;
}

.container {
  width: 80%;
  margin: 0 auto;
}

.text-danger {
  color: red;
}

.text-succes {
  color: green;
}
</style>
