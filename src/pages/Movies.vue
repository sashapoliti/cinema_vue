<template>
  <div class="container">
    <!-- <div class="title d-flex align-items-center">
      <img class="icon" src="/images/movie.png" alt="Movie section" />
      <img class="text" src="/images/movie-title.png" alt="Movie title" />
    </div> -->
    <div class="row g-3 pt-5">
      <div class="col-3" v-for="movie in movies" :key="movie.slug">
        <MovieComponent :movie="movie" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { store } from "../store";
import MovieComponent from "../components/MovieComponent.vue";

export default {
  name: "Movies",
  components: {
    MovieComponent,
  },
  data() {
    return {
      store,
      movies: [],
    };
  },
  methods: {
    getMovies() {
      axios.get(this.store.apiBaseUrl + "/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data.results;
      });
    },
  },
  mounted() {
    this.getMovies();
  },
};
</script>

<style lang="scss" scoped>
.title {
  margin-bottom: 20px;
  .icon {
    width: 70px;
  }
  .text {
    width: 200px;
  }
}
</style>
