<template>
  <div class="d-flex flex-wrap justify-content-center gap-5 h-100">
    <div class="card" style="width: 18rem" v-for="film in filmList" :key="film.id" >
      <img
        :src="`https://image.tmdb.org/t/p/original/${film.poster_path}`"
        class="card-img-top"
        alt="Film Poster"
      />
      <div class="card-body">
        <h5 class="card-title">{{film.title}}</h5>
        <span class="card-text">
         {{ film.original_title }}
        </span>
      </div>
      <ul class="list-group list-group-flush">
        <li class="list-group-item">{{film.original_language}}</li>
        <li class="list-group-item">IMDb: {{film.vote_average}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "FilmSearchResult",
  components: {},
  data() {
    return {
      filmList: [],
      UserSearch: "El Camino",
    };
  },
  methods: {
    searchFilm() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=1fc772f6f07f1b259cdb59ee1f2e79fb&query=" +
            this.UserSearch
        )
        .then((response) => {
          this.filmList = response.data.results;
        });
    },
  },
  mounted() {
    this.searchFilm();
  },
};
</script>

<style></style>
