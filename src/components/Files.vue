<template>
  <div class="files" v-if="isLoaded">
    <div class="file" v-for="(item, index) in files" :key="index">{{ item.name }}</div>
  </div>
  <div v-else>
    <p>Loading files...</p>
  </div>
</template>

<script>
import { Dropbox } from "dropbox";
export default {
  name: "Files",
  props: {
    token: String
  },
  data: function() {
    return {
      isLoaded: false,
      files: {}
    }
  },
  mounted() {
    this.getFiles(this.token);
  },
  methods: {
    getFiles(token) {
      var dbx = new Dropbox({ accessToken: token, fetch: fetch });
      dbx.filesListFolder({ path: "" }).then(response => {
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
