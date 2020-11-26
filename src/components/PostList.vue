<template>
  <h2 v-if="loadingProp">Loading.... / Chargement....</h2>
  <ul>
    <li v-for="currentPost in postsProp" v-bind:key="currentPost.id">
      {{currentPost.title}}
    </li>
  </ul>
</template>

<script>
export default {
  name: "PostList",
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