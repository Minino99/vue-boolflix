<template>
  <div class="headercontainer">
    <div class="container p-3 d-flex justify-content-between">
      <div><h1 class="color-danger">BOOLFLIX</h1></div>
      <div class="input-group">
        <input
          type="text"
          class="form-control"
          placeholder="Inserisci il nome del film"
          v-model="UserSearch"
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
            `https://api.themoviedb.org/3/search/movie?api_key=1fc772f6f07f1b259cdb59ee1f2e79fb&query=${this.UserSearch}`
          )
          .then((response) => {
            state.films = response.data.results;
            console.log(state.films);
          });
    },
  },
};
</script>

<style lang="scss" scoped>
.headercontainer {
  background-color: #3e333f;
  color: #fc4442;
}

.input-group {
  width: fit-content;
}
</style>
