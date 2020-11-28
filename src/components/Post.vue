<template>
  <li>
    {{currentPostProp.title}}
  </li>
</template>

<script>
export default {
  name: "Post",
  props: {
    currentPostProp: {
      type: Object,
      required: true,
    },
  },
  created() {
    console.log(this.currentPostProp);
  },
};
</script>

<style>
</style>