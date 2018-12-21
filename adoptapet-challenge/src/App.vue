<template>
  <div id="app">
    <Autosuggest />
  </div>
</template>

<script>
import Autosuggest from './components/Autosuggest.vue'

export default {
  name: 'app',
  components: {
    Autosuggest
  }
}
</script>

<style lang="scss">
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height: 100%;
}
</style>
