<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App" />
</template>

<script>
import axios from "axios";
import HelloWorld from "./components/HelloWorld.vue";
export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      posts: [],
      loading: false,
      //pagination variables
      currentPage: 1,
      postsPerPage: 10,
    };
  },
  methods: {
    async fetchPosts() {
      this.loading = true;
      const response = await axios.get(
        "https://jsonplaceholder.typicode.com/posts"
      );
      const data = response.data;
      console.log(data);
      this.loading = false;
    },
  },
  async created() {
    this.fetchPosts();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
