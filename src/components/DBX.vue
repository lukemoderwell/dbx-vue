<template>
  <div>
    <svg class="maestro-nav__logo" aria-label="Home" xmlns="http://www.w3.org/2000/svg" role="img" width="32px" height="32px" viewBox="0 0 32 32" style="fill:#0062ff;" data-reactid="12"><title data-reactid="13"></title><path d="M8 2.4l8 5.1-8 5.1-8-5.1 8-5.1zm16 0l8 5.1-8 5.1-8-5.1 8-5.1zM0 17.7l8-5.1 8 5.1-8 5.1-8-5.1zm24-5.1l8 5.1-8 5.1-8-5.1 8-5.1zM8 24.5l8-5.1 8 5.1-8 5.1-8-5.1z" data-reactid="14"></path></svg>
    <div v-if="isAuthed">
      <p>Hello, {{dbxData.user.name.given_name}}</p>
    </div>
    <div v-else>
      <a href="#" id="authlink" style="background: #1268FB">Sign in with Dropbox</a>
    </div>
  </div>
</template>

<script>
import { Dropbox } from "dropbox";

// get data from Dropbox and add to Vue
var ACCESS_TOKEN = process.env.VUE_APP_DB_ACCESS_TOKEN;
var CLIENT_ID = process.env.VUE_APP_DB_KEY;
var dbx = new Dropbox({ accessToken: ACCESS_TOKEN, clientId: CLIENT_ID, fetch: fetch });

function getUrlParams( prop ) {
    var params = {};
    var search = decodeURIComponent( window.location.href.slice( window.location.href.indexOf( '?' ) + 1 ) );
    var definitions = search.split( '&' );

    definitions.forEach( function( val ) {
        var parts = val.split( '=', 2 );
        params[ parts[ 0 ] ] = parts[ 1 ];
    } );

    return ( prop && prop in params ) ? params[ prop ] : params;
}

export default {
  name: "DBX",
  mounted() {
    this.setupAuth();
  },
  data: function() {
    return {
      isAuthed: false,
      isLoading: false,
      dbxData: {}
    };
  },
  methods: {
    setupAuth() {
      var authUrl = dbx.getAuthenticationUrl('http://localhost:8080/');
      document.getElementById('authlink').href = authUrl;
      this.checkAuthStatus();
    },
    checkAuthStatus() {
      var params = getUrlParams('access_token');
      var token = params['http://localhost:8080/#access_token'];
      if (token !== undefined) {
        this.isAuthed = true;
        this.getData(token);
      }
    },
    getData(token) {
      this.isLoading = true;
      var dbx = new Dropbox({ accessToken: token, fetch: fetch });
      console.log(dbx);
      dbx.usersGetCurrentAccount().then(response => {
        this.dbxData.user = response;
      });
      // list out all folders
      dbx.filesListFolder({ path: "" }).then(response => {
        this.dbxData.directories = response.entries;
        this.isLoading = false;
      });
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
  padding: 1rem;
  background: lightblue;
}

#authlink {
  display: inline-block;
  margin-top: 1rem;
  padding: .5rem .85rem;
  color: white;
  text-decoration: none;
}
</style>
