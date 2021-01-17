<template>
  <div id="app">
    <!-- <v-select 
      :options="options"
      @select="optionSelect"
      :selected="selected"
    /> -->
    <!-- <p>Selected option goes here:{{ selected }}</p> -->
    <v-main-wrapper />
  </div>
</template>

<script>
  
import VMainWrapper from './components/v-main-wrapper.vue'
// import vSelect from './components/v-select'

export default {
  name: 'App',
  components: {
    VMainWrapper
  },
  data() {
    return {
      options: [
        {name: 'Option 1', value: 1},
        {name: 'Option 2', value: 2},
        {name: 'Option 3', value: 3},
        {name: 'Option 4', value: 4},
        {name: 'Option 5', value: 5}
      ],
      selected: 'Select'
    }
  },
  methods: {
    optionSelect(option) {
      this.selected = option.name
    }
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
