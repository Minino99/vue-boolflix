<template>
  <div id="app">
    <TheHeader/>
    <TheBody/>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue'
import TheBody from './components/TheBody.vue'

export default {
  name: 'App',
  components: {
    TheHeader, TheBody
},
}
</script>

<style lang="scss">
@import "~@fortawesome/fontawesome-free/css/all.min.css";

#app{
  height: 100vh;
  background-color: #810000;
}
</style>
