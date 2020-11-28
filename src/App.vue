<template>
  <PostList v-bind:postsProp="currentPosts" v-bind:loadingProp="loading" />
  <!-- NEW: The paginate-evt being passed up from the child Pagination component, which is bring with it the current page number data - which we are accessing via $event. -->
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
    //NEW: We then assign the currentPage to that $event coming from the child, but obviously the parametre is simply called currentPageNumber. $event is the arguement and currentPageNumber is the parametre just in case this is confusing to me later on
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
