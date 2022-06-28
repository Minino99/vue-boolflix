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
        <button
          class="btn btn-danger"
          type="button"
          @click="pushInput"
        >
          Cerca
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import {UserInput} from "../store.js";
export default {
  name: "TheHeader",
  components: {},
  data() {
    return {
     UserSearch: "",
    };
  },
  methods: {
   pushInput() {
     UserInput = this.UserSearch;
   },
  }
};
</script>

<style lang="scss" scoped>

.headercontainer{
 background-color: #3E333F;
 color: #FC4442;
}

.input-group {
  width: fit-content;
}

</style>
