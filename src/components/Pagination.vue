<template>
  <div class="container">
    <nav>
      <ul class="pagination justify-content-end">
        <li class="page-item" :class="{ disabled: prevPageToken === undefined }">
          <a class="page-link" href="#" aria-label="Previous" @click="prevPage">
            <span aria-hidden="true">&laquo; Previous</span>
          </a>
        </li>

        <li class="page-item" :class="{ disabled: nextPageToken === undefined }">
          <a class="page-link" href="#" aria-label="Next" @click="nextPage">
            <span aria-hidden="true">Next &raquo;</span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Pagination",
  methods: {
    prevPage() {
      this.$emit("prev-page");
    },
    nextPage() {
      this.$emit("next-page");
    }
  },
  props: ["prevPageToken", "nextPageToken"]
};
</script>

<style scoped>
.page-link {
  box-shadow: none !important;
}
</style>