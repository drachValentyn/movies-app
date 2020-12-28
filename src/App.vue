<template>
  <div id="app">
    <Loader />
    <Notification />
    <PosterBg :poster="posterBg" />
    <Header />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
    <MoviesPagination
      :total="moviesLength"
      :per-page="moviesPerPage"
      :current-page="currentPage"
      @pageChanged="onPageChanged"
    />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import MoviesList from "@/components/MoviesList";
import PosterBg from "@/components/PosterBg";
import MoviesPagination from "@/components/MoviesPagination";
import Loader from "@/components/Loader";
import Header from "@/components/Header";
import Notification from "@/components/Notification";

export default {
  name: "App",
  components: {
    MoviesList,
    PosterBg,
    MoviesPagination,
    Loader,
    Header,
    Notification
  },
  data: () => ({
    posterBg: ""
  }),
  watch: {
    "$route.query": {
      handler: "onPageQueryChanged",
      immediate: true,
      deep: true
    }
  },
  computed: {
    ...mapGetters("movies", [
      "moviesList",
      "moviesLength",
      "currentPage",
      "moviesPerPage"
    ])
  },
  methods: {
    ...mapActions("movies", ["changeCurrentPage"]),

    onPageQueryChanged({ page = 1 } = {}) {
      this.changeCurrentPage(+page);
    },
    onChangePoster(poster) {
      this.posterBg = poster;
    },
    onPageChanged(page) {
      this.$router.push({ query: { page } });
    }
  }
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
}
</style>
