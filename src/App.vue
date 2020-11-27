<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <PostList v-bind:postsProp="currentPosts" v-bind:loadingProp="loading" />
  <Pagination v-bind:postsPerPageProp="postsPerPage" v-bind:postsLengthProp="posts.length" v-on:paginate-evt="paginate($event)" />
</template>

<script>
import axios from "axios";
import PostList from "./components/PostList";
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

      this.posts = data;
      this.loading = false;
    },
    //NEW:
    paginate(currentPageNumber) {
      console.log(currentPageNumber);
      this.currentPage = currentPageNumber;
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
