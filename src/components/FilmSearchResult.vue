<template>
  <div class="d-flex flex-wrap justify-content-center gap-5 h-100">
    <div
      class="card"
      style="width: 18rem"
      v-for="film in filterFilms"
      :key="film.id"
    >
      <img
        :src="`https://image.tmdb.org/t/p/original/${film.poster_path}`"
        class="card-img-top"
        alt="Film Poster"
      />
      <div class="card-body">
        <h5 class="card-title">{{ film.title }}</h5>
        <span class="card-text text-muted">
          {{ film.original_title }}
        </span>
      </div>
      <ul class="list-group list-group-flush">
        <li class="list-group-item"><img :src="`https://unpkg.com/language-icons/icons/${film.original_language}.svg`" :alt="film.original_language" srcset=""></li>
        <li class="list-group-item">IMDb: {{ film.vote_average }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { state } from "@/store";

export default {
  name: "FilmSearchResult",
  components: {},
  data() {
    return {};
  },
  computed: {
    filterFilms() {
      return state.films;
    },
  },
};
</script>

<style lang="scss">
.card {
  color: #1B1717;
  border: 3px solid #EEEBDD !important;
  background-color: #EEEBDD !important;

  .list-group-item {
    color: #1B1717 !important;
    background-color: #EEEBDD !important;
    img{
      width: 30px;
      border-radius: 50%;
    }
  }
}

.text-muted {
  font-size: 0.7rem;
}
</style>
