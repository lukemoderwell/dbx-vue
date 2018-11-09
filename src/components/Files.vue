<template>
  <div class="files">
    <div class="file" v-for="item in files">{{ item.name }}</div>
  </div>
</template>

<script>
export default {
  name: "Files",
  props: {
    files: Object
  }
};
</script>

<style>
  .file {
    margin: .5rem 0;
  }
</style>
