<template>
  <nav>
    <ul>
      <li v-for="currentPageNumber in pageNumbers" v-bind:key="currentPageNumber">
        <!-- NOTE: In the next branch, we will make it work upon click. We will put a click event in this anchor tag. For now it only works by changing the currentPage in our code (change value of currentPage @ App.js) -->
        <a href="#">{{currentPageNumber}}</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    postsPerPageProp: {
      type: Number,
      required: true,
    },
    // NOTE: This is the length of ALL the posts
    postsLengthProp: {
      type: Number,
      required: true,
    },
  },
  computed: {
    // NOTE: This is the number of page links there will be. Look at the li element at the template code.
    pageNumbers() {
      const pageNumbers = [];

      // NOTE: so in our default case, we have 100 posts and there will be 10 posts per page. So 100/10 = 10. If we suddenly have 5 posts per page, there will be 20 page links (100/5).
      let pageNumLimit = Math.ceil(
        this.postsLengthProp / this.postsPerPageProp
      );

      for (let i = 1; i <= pageNumLimit; i++) {
        pageNumbers.push(i);
      }

      return pageNumbers;
    },
  },
  created() {
    console.log("Pagination component created. TESTO");
  },
};
</script>

<style>
</style>
