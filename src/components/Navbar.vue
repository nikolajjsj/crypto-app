<template>
  <div id="navbar">
    <router-link class="navbar__link" to="/">Home</router-link>
    <router-link class="navbar__link" to="/about">About</router-link>
    <span v-if="count"> number of hits: {{ count }} </span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      count: null
    }
  },
  async created () {
    const res = await fetch('https://api.countapi.xyz/hit/crypto-app/haus')
    const json = await res.json()
    this.count = json.value
  }
}
</script>

<style>
#navbar {
  padding: 30px;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  margin: 0 auto;
}

.navbar__link {
  font-weight: bold;
  color: #2c3e50;
  margin: 0 1em;
}

.navbar__link.router-link-exact-active {
  color: #42b983;
}
</style>
