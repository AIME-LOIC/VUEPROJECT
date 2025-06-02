<template>
  <div id="app">
    <h1>My Wishlist App</h1>
    <Wishlist />
  </div>
</template>

<script>
import Wishlist from './components/wishlist.vue'

export default {
  name: 'App',
  components: {
    Wishlist,
  },
}
</script>

<style>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 40px;
}
</style>
