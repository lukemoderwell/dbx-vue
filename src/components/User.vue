<template>
  <div class="user" v-if="isLoaded">
    <img class="user-img" :src="user.profile_photo_url">
    <span>{{user.name.given_name}} {{user.name.surname}}</span>
  </div>
  <div v-else>
    <p>Loading</p>
  </div>
</template>

<script>
import { Dropbox } from "dropbox";
export default {
  name: "User",
  props: {
    token: String
  },
  data: function() {
    return {
      isLoaded: false,
      user: {}
    }
  },
  mounted() {
    this.getUser(this.token);
  },
  methods: {
    getUser(token) {
      var dbx = new Dropbox({ accessToken: token, fetch: fetch });
      dbx.usersGetCurrentAccount().then(response => {
        this.user = response;
        this.isLoaded = true;
      });
    }
  }
};
</script>

<style>
.user {
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.user-img {
  margin-bottom: 1rem;
  min-width: 40px;
  height: 40px;
  border-radius: 50%;
}
</style>
