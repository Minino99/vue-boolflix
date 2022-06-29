<template>
  <div class="headercontainer">
    <div class="container p-3 d-flex justify-content-between gap-5 h-100">
      <div class="h-100"><a href=""><img src="../../public/img/logo.png" class="h-100" alt="" srcset=""></a></div>
      <div class="input-group">
        <input
          type="text"
          class="form-control"
          placeholder="Inserisci il nome del film"
          v-model="UserSearch"
          @keyup.enter="filterFilms"
        />
        <button class="btn btn-danger" type="button" @click="filterFilms">
          Cerca
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { state } from "../store.js";
export default {
  name: "TheHeader",
  components: {},
  data() {
    return {
      UserSearch: "",
    };
  },
  methods: {
    filterFilms() {
        axios
          .get(
            `https://api.themoviedb.org/3/search/movie?api_key=1fc772f6f07f1b259cdb59ee1f2e79fb&query=${this.UserSearch}&language=it-IT&page=1`
          )
          .then((response) => {
            state.films = response.data.results;
            console.log(state.films);
          });
    },
  },
  mounted(){
    axios
      .get(
        `https://api.themoviedb.org/3/movie/popular?api_key=1fc772f6f07f1b259cdb59ee1f2e79fb&language=it-IT&page=1`
      )
      .then((response) => {
        state.films = response.data.results;
        console.log(state.films);
      });
  }
};
</script>

<style lang="scss" scoped>
.headercontainer {
  background-color: #EEEBDD;
  color: #fc4442;
  height: 88px;
}

.input-group {
  width: fit-content;
}
</style>
