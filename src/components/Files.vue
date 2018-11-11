<template>
  <div class="files" v-if="isLoaded">
    <div class="file" v-for="(item, index) in files" :key="index">{{ item }}</div>
  </div>
  <div v-else>
    <p>Loading files...</p>
  </div>
</template>

<script>
import { Dropbox } from "dropbox";
var dbx;
export default {
  name: "Files",
  props: {
    token: String,
    path: String
  },
  data: function() {
    return {
      isLoaded: false,
      files: {}
    }
  },
  mounted() {
    dbx = new Dropbox({ accessToken: this.token, fetch: fetch });
    this.getFiles();
  },
  methods: {
    getFiles() {
      dbx.filesListFolder({ path: this.path }).then(response => {
        this.files = response.entries;
        this.isLoaded = true;
      });
    }
  }
};
</script>

<style>
.file {
  margin: 0.5rem 0;
}
</style>
