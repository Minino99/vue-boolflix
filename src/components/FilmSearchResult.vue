<template>
  <div class="d-flex flex-wrap justify-content-center gap-5 h-100">
    <div
      class="card"
      style="width: 18rem"
      v-for="film in filterFilms"
      :key="film.id"
    >
      <img
        :src="`https://image.tmdb.org/t/p/w342/${film.poster_path}`"
        class="card-img-top"
        alt="Film Poster"
      />
      <ul class="list-group list-group-flush">
        <li class="list-group-item">
          <h5 class="card-title">{{ film.title }}</h5>
        </li>
        <li class="list-group-item">
          <span class="card-text text-muted">
            {{ film.original_title }}
          </span>
        </li>
        <li class="list-group-item">
          <img
            :src="`https://unpkg.com/language-icons/icons/${film.original_language}.svg`"
            :alt="film.original_language"
            srcset=""
          />
        </li>
        <li class="list-group-item">{{ getStars(film.vote_average) }}</li>
      </ul>
    </div>
    <div
      class="card"
      style="width: 18rem"
      v-for="serie in filterTvSeries"
      :key="serie.id"
    >
      <img
        :src="`https://image.tmdb.org/t/p/w342/${serie.poster_path}`"
        class="card-img-top"
        alt="Film Poster"
      />
      <ul class="list-group list-group-flush">
        <li class="list-group-item">
          <h5 class="card-title">{{ serie.name }}</h5>
        </li>
        <li class="list-group-item">
          <span class="card-text text-muted">
            {{ serie.original_name }}
          </span>
        </li>
        <li class="list-group-item">
          <img
            :src="`https://unpkg.com/language-icons/icons/${serie.original_language}.svg`"
            :alt="serie.original_language"
            srcset=""
          />
        </li>
        <li class="list-group-item">{{ getStars(serie.vote_average) }}</li>
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
  methods: {
    getStars(vote){
      vote = Math.round(vote /2);
      return (`⭐`).repeat(vote);
    }
  },

  computed: {
    filterFilms() {
      return state.films;
    },
    filterTvSeries() {
      return state.tvSeries;
    },
  },
};
</script>

<style lang="scss">
.card {
  color: #1b1717;
  border: 3px solid #eeebdd !important;
  background-color: #eeebdd !important;
  position: relative;
  cursor: pointer;
  height: fit-content;
}

.list-group-item {
  color: #1b1717 !important;
  background-color: #eeebdd !important;
  img {
    width: 30px;
    border-radius: 50%;
  }
}

.list-group {
  width: 100%;
  position: absolute;
  bottom: 0;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}

.card:hover .list-group {
  opacity: 0.9;
}

.text-muted {
  font-size: 0.7rem;
}
</style>
