<template>
<v-container>
  <v-layout>
    <v-flex md10 offset-md1>
      <canvas
        class="canvas"
        ref="canvas"
        @mousedown="penDown"
        @mousemove="penMove"
        @mouseup="penUp"
        @mouseleave="penUp">
      </canvas>
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
export default {
  props: ['socket'],
  name: 'Canvas',
  data () {
    return {
      canvas: null,
      ctx: null,
      prevX: 0,
      prevY: 0,
      currX: 0,
      currY: 0,
      contact: false
    }
  },
  created () {
    window.addEventListener('resize', this.handleResize)
  },
  mounted () {
    this.canvas = this.$refs.canvas
    this.ctx = this.canvas.getContext('2d')
    this.handleResize()
    this.socket.on('draw', this.onDrawEvent)
  },
  destroyed () {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    penDown (event) {
      this.contact = true
    },
    penMove (event) {
      if (this.contact) {
        this.drawLine(this.prevX, this.currX, this.prevY, this.currY, false)
      }
      this.updateCoords(event)
    },
    penUp (event) {
      this.contact = false
    },
    drawLine (x0, x1, y0, y1, emit) {
      this.ctx.beginPath()
      this.ctx.moveTo(x0, y0)
      this.ctx.lineTo(x1, y1)
      this.ctx.stroke()
      this.ctx.closePath()

      if (emit) {
        return
      }

      var w = this.ctx.canvas.width
      var h = this.canvas.height

      this.socket.emit('draw', {
        x0: x0 / w,
        x1: x1 / w,
        y0: y0 / h,
        y1: y1 / h
      })
    },
    updateCoords (event) {
      var rect = this.canvas.getBoundingClientRect()
      this.prevX = this.currX
      this.prevY = this.currY
      this.currX = event.clientX - rect.left
      this.currY = event.clientY - rect.top
    },
    handleResize () {
      this.ctx.canvas.width = 2 * window.innerWidth / 3
      this.ctx.canvas.height = 2 * window.innerHeight / 3
    },
    onDrawEvent (data) {
      var w = this.ctx.canvas.width
      var h = this.ctx.canvas.height
      console.log('drawing')
      this.drawLine(data.x0 * w, data.x1 * w, data.y0 * h, data.y1 * h, true)
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .canvas {
    border-style: solid;
    border-width: 1px;
  }
</style>
