<template>
  <div id="app">
    <ColorPicker :color="color" />
    <Canvas :pixels="pixels"/>
  </div>
</template>

<script>
import ColorPicker from './components/ColorPicker.vue'
import Canvas from './components/Canvas.vue'

const defaultColor = 'white'

export default {
  name: 'App',
  components: {
    ColorPicker,
    Canvas
  },
  data() {
    return {
      color: defaultColor,
      pixels: Array(30 * 30)
        .fill()
        .map(() => defaultColor)
    }
  },
  mounted() {
    this.$root.$on('updateColor', color => {
      this.color = color
    })
    this.$root.$on('clickedpixel', index => {
      this.pixels.splice(index, 1, this.color)
    })
  }
}
</script>

<style>
#app {
  font: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
