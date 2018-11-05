<template>
  <div class="gallery">
    <div class="gallery-unit"></div>
    <div class="gallery-unit"></div>
    <div class="gallery-unit"></div>
    <div class="gallery-unit"></div>
  </div>
</template>

<script>
export default {
  name: 'Gallery',
  props: {
    text: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gallery {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 800px;
  padding-left: 1rem;
  padding-right: 1rem;
  overflow-y: auto;
}

.gallery-unit {
  width: 25%;
  background: cadetblue;
}
</style>
