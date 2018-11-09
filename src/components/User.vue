<template>
  <div class="user">
    <img class="user-img" :src="user.profile_photo_url">
    <span>{{user.name.given_name}}</span>
  </div>
</template>

<script>
export default {
  name: "User",
  props: {
    user: Object
  }
};
</script>

<style>
.user {
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
.user-img {
  margin-right: 1rem;
  min-width: 40px;
  height: 40px;
  border-radius: 50%;
}
</style>
