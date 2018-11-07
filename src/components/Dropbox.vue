<template>
  <div>
    <svg class="maestro-nav__logo" aria-label="Home" xmlns="http://www.w3.org/2000/svg" role="img" width="32px" height="32px" viewBox="0 0 32 32" style="fill:#0062ff;" data-reactid="12"><title data-reactid="13"></title><path d="M8 2.4l8 5.1-8 5.1-8-5.1 8-5.1zm16 0l8 5.1-8 5.1-8-5.1 8-5.1zM0 17.7l8-5.1 8 5.1-8 5.1-8-5.1zm24-5.1l8 5.1-8 5.1-8-5.1 8-5.1zM8 24.5l8-5.1 8 5.1-8 5.1-8-5.1z" data-reactid="14"></path></svg>
    <div v-if="isLoading">
      <p>Loading...</p>
    </div>
    <div v-else>
      <p>Hello, {{dbx.user.name.given_name}}</p>
      <div class="directories">
        <div v-for="item in dbx.directories">
          <div class="directory">{{ item.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Dropbox } from "dropbox";

// get data from Dropbox and add to Vue
var ACCESS_TOKEN = process.env.VUE_APP_DB_ACCESS_TOKEN;
var dbx = new Dropbox({ accessToken: ACCESS_TOKEN, fetch: fetch });

export default {
  name: "Dropbox",
  mounted() {
    this.getData();
  },
  data: function() {
    return {
      isLoading: false,
      dbx: {}
    };
  },
  methods: {
    getData() {
      this.isLoading = true;
      dbx.usersGetCurrentAccount().then(response => {
          this.dbx.user = response;
        }).catch(err => (this.isLoading = false));
      // list out all folders
      dbx.filesListFolder({ path: "" }).then(response => {
          this.dbx.directories = response.entries;
          this.isLoading = false;
        }).catch(err => (this.isLoading = false));
    }
  }
};
</script>

<style>
.directories {
  display: flex;
  flex-wrap: wrap;
  padding: 1rem;
}

.directory {
  width: 200px;
  height: 200px;
  margin: 1rem;
  background: lightblue;
}
</style>
