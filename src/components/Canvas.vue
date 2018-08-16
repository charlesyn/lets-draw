<template>
  <v-layout>
    <v-flex>
      <canvas
        class="canvas"
        ref="canvas"
        @mousedown="penDown"
        @mousemove="penMove"
        @mouseup="penUp"
        @mouseleave="penUp">
      </canvas>
    </v-flex>
    <v-flex>
      <draw-tools id='drawTools' :canvas='canvas' :ctx='ctx' :socket='socket'/>
    </v-flex>
  </v-layout>
</template>

<script>
import DrawTools from './DrawTools'

export default {
  components: {
    DrawTools
  },
  props: ['socket'],
  name: 'Canvas',
  data () {
    return {
      canvas: null,
      ctx: null,
      contact: false,
      points: []
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
    this.socket.on('clearCanvas', this.clearCanvas)
    this.ctx.lineJoin = this.ctx.lineCap = 'round'
    this.lineWidth = 10
  },
  destroyed () {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    penDown (event) {
      this.contact = true
      this.points.push({ x: event.clientX, y: event.clientY })
    },
    penMove (event) {
      if (!this.contact) {
        return
      }
      this.points.push({ x: event.clientX, y: event.clientY })
      this.drawLine(this.points)
    },
    penUp (event) {
      this.contact = false
      this.emitLine()
      this.points.length = 0
    },
    drawLine (points) {
      if (points.length < 1) {
        return
      }
      this.ctx.beginPath()
      this.ctx.moveTo(points[0].x, points[0].y)
      for (let i = 1; i < points.length; i++) {
        this.ctx.lineTo(points[i].x, points[i].y)
      }
      this.ctx.stroke()
    },
    emitLine () {
      this.socket.emit('draw', {
        points: this.points,
        style: this.ctx.strokeStyle,
        lineWidth: this.ctx.lineWidth,
        gco: this.ctx.globalCompositeOperation
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
      this.ctx.canvas.width = window.innerWidth
      this.ctx.canvas.height = window.innerHeight
    },
    onDrawEvent (data) {
      const currentStyle = this.ctx.strokeStyle
      const currentWidth = this.ctx.lineWidth
      const currentGCO = this.ctx.globalCompositeOperation
      this.ctx.strokeStyle = data.style
      this.ctx.lineWidth = data.lineWidth
      this.ctx.globalCompositeOperation = data.gco
      this.drawLine(data.points)
      this.ctx.strokeStyle = currentStyle
      this.ctx.lineWidth = currentWidth
      this.ctx.globalCompositeOperation = currentGCO
    },
    clearCanvas (data) {
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .canvas {
    position: absolute;
    width: 100%;
    height: 100%;
  }
  #drawTools {
    position: absolute;
    bottom: 0;
  }
</style>
