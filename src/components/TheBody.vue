<template>
  <div class="container py-5 overflow-auto">
      <FilmSearchResult />
  </div>
</template>

<script>
import FilmSearchResult from "./FilmSearchResult.vue";
export default {
  name: "TheBody",
  components: {
    FilmSearchResult,
  },
};
</script>

<style>
.container {
  height: 90%;
}

</style>
