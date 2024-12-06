<template>
  <div id="app">
    <!-- <image-crop :options="options"></image-crop> -->
    <scroll-sample></scroll-sample>
  </div>
</template>

<script>
// import ImageCrop from './VueImageCrop.vue'
import ScrollSample from './ScrollSample.vue'

export default {
  name: 'App',
  components: {
    // ImageCrop,
    ScrollSample
  },
  data() {
    return {
      options: {
        base: {
          width: 600,
          height: 300
        },
        img: {
          path: require('@/assets/crop-demo-image.jpg')
        }
      }
    }
  },
  mounted() {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
