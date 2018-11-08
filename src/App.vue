<template>
  <div id="app">
    <DBX />
  </div>
</template>

<script>
import DBX from './components/DBX.vue';

export default {
  name: 'app',
  components: {
    DBX
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
