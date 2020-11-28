<template>
  <nav>
    <ul>
      <li v-for="currentPageNumber in pageNumbers" v-bind:key="currentPageNumber">
        <a @click="paginate(currentPageNumber)">{{currentPageNumber}}</a>
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
    postsLengthProp: {
      type: Number,
      required: true,
    },
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
  //NEW: the paginate() below will take the current page number and pass an event up to the App component with that page number. In the App component, this page number will then be used to set the current page.
  //NOTE: This is Vue fundamentals: Event emission from child to parent. Still got it 😏
  methods: {
    paginate(pageNumber) {
      this.$emit("paginate-evt", pageNumber);
    },
  },
};
</script>

<style>
</style>
