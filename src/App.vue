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
#app{
  height: 100vh;
  background-color: #F2F2F2;
}
</style>
