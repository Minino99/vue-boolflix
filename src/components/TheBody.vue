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
  height: calc(100vh - 88px);
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.container::-webkit-scrollbar {
  display: none;
}
</style>
