<template>
  <div>
    <a href="/"><svg class="maestro-nav__logo" aria-label="Home" xmlns="http://www.w3.org/2000/svg" role="img" width="32px" height="32px" viewBox="0 0 32 32" style="fill:#0062ff;" data-reactid="12"><title data-reactid="13"></title><path d="M8 2.4l8 5.1-8 5.1-8-5.1 8-5.1zm16 0l8 5.1-8 5.1-8-5.1 8-5.1zM0 17.7l8-5.1 8 5.1-8 5.1-8-5.1zm24-5.1l8 5.1-8 5.1-8-5.1 8-5.1zM8 24.5l8-5.1 8 5.1-8 5.1-8-5.1z" data-reactid="14"></path></svg></a>
    <div v-if="this.hasToken">
      <User v-bind:token="this.accessToken" />
      <Files v-bind:token="this.accessToken" path="/photos/2018/10_october/crystal-slaughter-oct-18"/>
    </div>
    <div v-else>
      <a href="#" id="authlink" style="background: #1268FB">Sign in with Dropbox</a>
    </div>
  </div>
</template>

<script>
import { Dropbox } from "dropbox";
import User from "./User.vue";
import Files from "./Files.vue";
// get data from Dropbox and add to Vue
var ACCESS_TOKEN = process.env.VUE_APP_DB_ACCESS_TOKEN;
var CLIENT_ID = process.env.VUE_APP_DB_KEY;
var DOMAIN = process.env.VUE_APP_DOMAIN;

var dbx = new Dropbox({
  accessToken: ACCESS_TOKEN,
  clientId: CLIENT_ID,
  fetch: fetch
});

export default {
  name: "Signin",
  components: {
    User,
    Files
  },
  mounted() {
    this.setupAuth();
  },
  data: function() {
    return {
      hasToken: false,
      accessToken: ''
    };
  },
  methods: {
    setupAuth() {
      var authUrl = dbx.getAuthenticationUrl(DOMAIN);
      document.getElementById("authlink").href = authUrl;
      this.getToken();
    },
    getToken() {
      var params = this.getUrlParams("access_token");
      var token = params[DOMAIN + '#access_token'];
      this.accessToken = token;
      if (this.accessToken !== undefined) {
        this.hasToken = true;
      }
    },
    getUrlParams(prop) {
      var params = {};
      var search = decodeURIComponent(
        window.location.href.slice(window.location.href.indexOf("?") + 1)
      );
      var definitions = search.split("&");

      definitions.forEach(function(val) {
        var parts = val.split("=", 2);
        params[parts[0]] = parts[1];
      });

      return prop && prop in params ? params[prop] : params;
    }
  }
};
</script>

<style>
#authlink {
  display: inline-block;
  margin-top: 1rem;
  padding: 0.5rem 0.85rem;
  color: white;
  text-decoration: none;
}
</style>
