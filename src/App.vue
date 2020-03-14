<template>
  <div id="app">
    <Carousel></Carousel>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue'


    

export default {
  name: 'App',
  components: {
    Carousel,
  },


}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}
</style>
