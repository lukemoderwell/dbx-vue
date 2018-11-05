<template>
  <div id="app">
    <Title text="Exploring the DBX api"/>
    <Gallery />
  </div>
</template>

<script>
import Title from './components/Title.vue'
import Gallery from './components/Gallery.vue'

export default {
  name: 'app',
  components: {
    Title,
    Gallery
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  overflow: hidden;
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
