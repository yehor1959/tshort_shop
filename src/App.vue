<template>
  <div id="app">
    <p>Hello World!</p>
    <v-main-wrapper />
  </div>
</template>

<script>
  
import VMainWrapper from './components/v-main-wrapper.vue'

export default {
  name: 'App',
  components: {
    VMainWrapper
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
  margin-top: 60px;
}
</style>
