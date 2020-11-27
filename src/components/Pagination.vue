<template>
  <nav>
    <ul>
      <li v-for="currentPageNo in pageNumbers" v-bind:key="currentPageNo">
        <a @click="paginate(currentPageNo)">{{currentPageNo}}</a>
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
  data() {
    return {
      // pageNumbers: [],
    };
  },
  computed: {
    pageNumbers() {
      const pageNumbers = [];
      let pageNumLimit = Math.ceil(
        this.postsLengthProp / this.postsPerPageProp
      );

      for (let i = 1; i <= pageNumLimit; i++) {
        pageNumbers.push(i);
      }

      return pageNumbers;
    },
  },
  //NEW:
  methods: {
    paginate(pageNumber) {
      this.$emit("paginate-evt", pageNumber);
    },
  },
  created() {
    console.log("Pagination component created. TESTO");
  },
};
</script>

<style>
</style>
