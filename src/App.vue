<template>
  <div id="app">
    <searchbar @searchMovies="onSearchMovies"></searchbar>
    <div class="row">
      <div class="col" v-if="movieList.length > 0">
        <h2>Movies</h2>
        <div>
          <cards v-for="movie in movieList" :key="movie.id" :movie="movie"></cards>
        </div>
      </div>

      <div class="col" v-if="seriesList.length > 0">
        <h2>Serie tv</h2>

        <div>
          <cards v-for="serie in seriesList" :key="serie.id" :movie="serie"></cards>
        </div>
      </div>
  </div>
</template>

<script>
import axios from "axios";
import Searchbar from './components/Searchbar.vue'
import Cards from './components/Cards.vue';


export default {
  name: 'App',
  components: {
    Searchbar,
    Cards
  },
  data() {
    return {
      apiKey: "7c73cfda3c007d30235d95e81c7d945c",
      apiUrl: "https://api.themoviedb.org/3",
      movieList: [],
      seriesList: [],
      flags: {
        en: require("svg-country-flags/png100px/gb.png"),
        it: require("svg-country-flags/png100px/it.png"),
      },
    }
  },
  methods: {
    fetchData() {

    },
    onSearchMovies(url, textToSearch, dataKey) {
      axios
        .get(this.apiUrl + url, {
          params: {
            api_key: this.apiKey,
            query: textToSearch,
            language: "it",
          },
        })
        .then((resp) => {
          this[dataKey] = resp.data.results;
        });
    }
  },
  mounted() {
   /* axios.get(this.apiUrl + "/search/movie", {
      params: {
        api_key: this.apiKey,
        query: "ciao",
      }, 
    }).then((resp) => {
      this.movieList = resp.data.results;
    });*/
  }
}
</script>

<style lang="scss">
@import "@/styles/app";
</style>
