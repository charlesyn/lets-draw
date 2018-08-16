<template>
  <v-toolbar dense floating>
    <v-btn-toggle v-model='toggle' mandatory>
      <v-btn icon @click='usePencil'>
        <v-icon>create</v-icon>
      </v-btn>
      <v-btn icon @click='useBrush'>
        <v-icon>brush</v-icon>
      </v-btn>
      <v-btn icon @click='useEraser'>
        <v-icon>web_asset</v-icon>
      </v-btn>
    </v-btn-toggle>
    <v-btn icon @click='clearCanvas'>
      <v-icon>clear</v-icon>
    </v-btn>
  </v-toolbar>
</template>
<script>
export default {
  props: ['canvas', 'ctx', 'socket'],
  name: 'DrawTools',
  data () {
    return {
      toggle: 0,
      currentToggle: 0
    }
  },
  methods: {
    usePencil () {
      this.ctx.globalCompositeOperation = 'source-over'
      this.ctx.strokeStyle = 'black'
      this.ctx.lineWidth = 1
    },
    useBrush () {
      this.ctx.globalCompositeOperation = 'source-over'
      this.ctx.strokeStyle = 'black'
      this.ctx.lineWidth = 10
    },
    useEraser () {
      this.ctx.globalCompositeOperation = 'destination-out'
      this.ctx.strokeStyle = 'rgba(0,0,0,100)'
      this.ctx.lineWidth = 10
    },
    clearCanvas () {
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
      this.socket.emit('clearCanvas')
    }
  }
}
</script>
<style scoped>

</style>
