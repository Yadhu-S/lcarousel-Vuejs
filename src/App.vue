<template>
  <div id="app">
    <slides></slides>
  </div>
</template>

<script>
import Slides from './components/Slides'

export default {
  name: 'app',
  components: {
    Slides
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
