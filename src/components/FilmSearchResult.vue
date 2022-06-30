<template>
  <div class="d-flex flex-wrap justify-content-center gap-5 h-100">
    <div
      class="card"
      style="width: 18rem"
      v-for="film in filterFilms"
      :key="film.id"
    >
      <img
        :src="posterPlaceholder(film.poster_path)"
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
        <li class="list-group-item">
          <i
            class="fa-solid fa-star"
            v-for="index in getStars(film.vote_average)"
            :key="`stellapienafilm${index}`"
          ></i>
          <i
            class="fa-regular fa-star"
            v-for="index in emptyStars(film.vote_average)"
            :key="`stellavuotafilm${index}`"
          ></i>
        </li>
        <li class="list-group-item">
          <span
            class="card-text text-muted"
            v-for="genre in film.genre_ids"
            :key="`serietv-id${genre}`"
          >
            {{ `${getGenre(genre)},` }}
          </span>
        </li>
        <li class="list-group-item">
          <span
            class="card-text text-muted"
            v-for="index in 5"
            :key="`actor-id-${index}`"
          >
            {{ getActors(film.id, index) }}
          </span>
        </li>
      </ul>
    </div>
    <div
      class="card"
      style="width: 18rem"
      v-for="serie in filterTvSeries"
      :key="serie.id"
    >
      <img
        :src="posterPlaceholder(serie.poster_path)"
        class="card-img-top"
        alt="Serie Poster"
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
        <li class="list-group-item">
          <i
            class="fa-solid fa-star"
            v-for="index in getStars(serie.vote_average)"
            :key="`stellapienaserie${index}`"
          ></i>
          <i
            class="fa-regular fa-star"
            v-for="index in emptyStars(serie.vote_average)"
            :key="`stellavuotaserie${index}`"
          ></i>
        </li>
        <li class="list-group-item">
          <span
            class="card-text text-muted"
            v-for="genre in serie.genre_ids"
            :key="`serietv-id${genre}`"
          >
            {{ getGenre(genre) }}
          </span>
        </li>
        <li class="list-group-item">
          <span
            class="card-text text-muted"
            v-for="index in 5"
            :key="`actor-id-${index}`"
          >
            {{ getActorsTv(serie.id, index) }}
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { state } from "@/store";
import axios from "axios";

export default {
  name: "FilmSearchResult",
  components: {},
  data() {
    return {};
  },
  methods: {
    posterPlaceholder(poster) {
      if (
        `https://image.tmdb.org/t/p/w342/${poster}` !==
        "https://image.tmdb.org/t/p/w342/null"
      ) {
        return `https://image.tmdb.org/t/p/w342/${poster}`;
      } else {
        return "/img/imgError.png";
      }
    },
    getStars(vote) {
      vote = Math.round(vote / 2);
      return vote;
    },
    emptyStars(vote) {
      vote = Math.round(vote / 2);
      return 5 - vote;
    },
    getGenre(input) {
      for (let i = 0; i < state.genres.length; i++) {
        if (state.genres[i].id === input) {
          return state.genres[i].name;
        }
      }
    },
    getActorsTv(id, i) {
      axios
        .get(
          `https://api.themoviedb.org/3/tv/${id}/credits?api_key=1fc772f6f07f1b259cdb59ee1f2e79fb&language=it-IT`
        )
        .then((response) => {
          return response.data.cast[i].name;
        });
    },
    getActors(id, i) {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${id}/credits?api_key=1fc772f6f07f1b259cdb59ee1f2e79fb&language=it-IT`
        )
        .then((response) => {
          return response.data.cast[i].name;
        });
    },
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
.fa-star {
  color: #ce1212;
  padding-right: 5px;
}

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
