<template>
  <div id="app">
    <result-list></result-list>
  </div>
</template>

<script>
import ResultList from './components/ResultList.vue'

export default {
  name: 'App',
  components: {
    ResultList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 50%;
}
</style>
