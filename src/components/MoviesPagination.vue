<template>
  <div class="movies-pagination d-flex justify-content-center">
    <b-pagination
      v-model="currentPageModel"
      :per-page="perPage"
      :total-rows="total"
      aria-controls="my-table"
      prev-text="Prev"
      next-text="Next"
    />
  </div>
</template>

<script>
export default {
  name: "MoviesPagination",
  props: {
    currentPage: {
      type: Number,
      default: 1
    },
    total: {
      type: Number,
      default: 1
    },
    perPage: {
      type: Number,
      default: 1
    }
  },
  computed: {
    currentPageModel: {
      get() {
        return this.currentPage;
      },
      set(value) {
        this.$emit("pageChanged", value);
      }
    }
  }
};
</script>

<style scoped>
.movies-pagination {
  margin-top: 30px;
}

.movies-pagination >>> .pagination .page-item .page-link {
  background-color: transparent;
  font-size: 12px;
  color: white;
  box-shadow: none;
}

.movies-pagination >>> .pagination .page-item.active .page-link {
  border-color: white;
  background-color: white;
  color: black;
}

.movies-pagination >>> .pagination .page-item.disabled .page-link {
  color: gray;
}
</style>
