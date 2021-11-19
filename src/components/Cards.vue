<template>
  <div class="row">
    <div class="col">
      <img class="movie_poster" :src="imgPath" alt="">
    </div>
    <div class="col">
      <div class="text-left mb-3">
        <div><strong>Titolo:</strong> {{ movieTitle }}</div>

        <div v-if="movieOriginalTitle">
          <strong>Titolo originale:</strong> {{ movieOriginalTitle }}
        </div>

        <div>
          <strong>Lingua: </strong>
          <span v-if="!flagsPath">{{ movie.original_language }} </span>
          <img v-else class="flag-icon" :src="flagsPath" alt="language flag">
        </div>

        <div>
          <strong>Voto: </strong>
          <div class="stars-container" style="display: inline-block">
            <i v-for="num in 5" :key="'vote_star_' + num" class="fa" :class="num <= vote ? 'fa-star' : 'fa-star-o'"></i>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
props: {
    movie: Object,
},
data() {
    return {
    flags: {
        es: require("svg-country-flags/png100px/es.png"),
        en: require("svg-country-flags/png100px/gb.png"),
        it: require("svg-country-flags/png100px/it.png"),
    },
    };
}, 
methods: {
    movieTitle() {
      return this.movie.title ? this.movie.title : this.movie.name;
    },
    movieOriginalTitle() {
      const originalName = this.movie.original_title
        ? this.movie.original_title
        : this.movie.original_name;
      return this.movieTitle === originalName ? "" : originalName;
    },
    imgPath() {
      const pathRoot = "https://image.tmdb.org/t/p/";
      const imgSize = "w342";
      if (!this.movie.poster_path) {
        return require("@/assets/logo.png");
        }
      return pathRoot + imgSize + this.movie.poster_path;
    },
    flagsPath() {
      return this.langFlags[this.movie.original_language];
    },
    vote() {
      return Math.round(this.movie.vote_average / 2);
    },
  },
}
</script>
    
<style scoped>
.flag-icon {
  width: 30px;
}
.movie-poster {
  width: 300px;
}
</style>