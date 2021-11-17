<template>
  <div id="app">
    <searchbar @searchMovies="onSearchMovies"></searchbar>
    <ul>
      <li v-for="movie in movieList" :key="movie.id">
        {{movie.title}} {{movie.original_title}} {{movie.vote_average}} {{movie.original_language}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Searchbar from './components/Searchbar.vue'


export default {
  name: 'App',
  components: {
    Searchbar
  },
  data() {
    return {
      apiKey: "7c73cfda3c007d30235d95e81c7d945c",
      apiUrl: "https://api.themoviedb.org/3",
      movieList: [],
    }
  },
  methods: {
    fetchData() {

    },
    onSearchMovies() {

    }
  },
  mounted() {
    axios.get(this.apiUrl + "/search/movie", {
      params: {
        api_key: this.apiKey,
        query: "ciao",
      }, 
    }).then((resp) => {
      this.movieList = resp.data.results;
    });
  }
}
</script>

<style lang="scss">
@import "@/styles/app";
</style>
