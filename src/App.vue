<template>
  <PostList v-bind:postsProp="currentPosts" v-bind:loadingProp="loading" />
  <!-- NEW: The pagination will accept two props from this app component. the posts per page and the total number of posts (the length of the posts array) -->
  <Pagination v-bind:postsPerPageProp="postsPerPage" v-bind:postsLengthProp="posts.length" />
</template>

<script>
import axios from "axios";
import PostList from "./components/PostList";
//NEW:
import Pagination from "./components/Pagination";
export default {
  name: "App",
  components: {
    PostList: PostList,
    Pagination: Pagination,
  },
  data() {
    return {
      posts: [],
      loading: false,
      // NOTE: Playing around with this value, will change the currentPage of the array of posts. We will write some code in the next branch so that we can change this value by clicking the correct page number
      currentPage: 1,
      // NOTE: playing around with this value will change the number of posts shown in a page. We're not touching this.
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

      this.posts = data;
      this.loading = false;
    },
  },
  computed: {
    indexOfLastPost() {
      return this.currentPage * this.postsPerPage;
    },
    indexOfFirstPost() {
      return this.indexOfLastPost - this.postsPerPage;
    },
    currentPosts() {
      return this.posts.slice(this.indexOfFirstPost, this.indexOfLastPost);
    },
  },
  async created() {
    this.fetchPosts();
  },
  //TESTING:
  updated() {
    console.log(this.currentPosts);
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
