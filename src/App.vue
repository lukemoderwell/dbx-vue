<template>
  <div id="app">
    <Dropbox />
  </div>
</template>

<script>
import Title from './components/Title.vue';
import Dropbox from './components/Dropbox.vue';

export default {
  name: 'app',
  components: {
    Dropbox
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
