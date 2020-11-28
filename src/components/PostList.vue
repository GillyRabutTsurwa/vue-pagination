<template>
  <h2 v-if="loadingProp">Loading.... / Chargement....</h2>
  <ul>
    <!-- <li v-for="currentPost in postsProp" v-bind:key="currentPost.id">
      {{currentPost.title}}
    </li> -->
    <CurrentPost v-for="currentPost in postsProp" v-bind:key="currentPost.id" v-bind:currentPostProp="currentPost" />
  </ul>
</template>

<script>
import Post from "./Post";
export default {
  name: "PostList",
  components: {
    CurrentPost: Post,
  },
  props: {
    postsProp: {
      type: Array,
      required: true,
    },
    loadingProp: {
      type: Boolean,
      required: false,
    },
  },
};
</script>

<style>
</style>