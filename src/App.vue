<template>
  <div id="app">
    <NavegableImage img="https://picsum.photos/id/259/2000/2000" imagezoom="1.8" alt="Lorem Ipsum" />
  </div>
</template>

<script>
import NavegableImage from './components/navegable-image.vue'

export default {
  name: 'app',
  components: {
    NavegableImage
  }
}
</script>

<style lang="scss">
#app {
  width: 500px;
  height: 500px;
  overflow: hidden;
}
</style>
