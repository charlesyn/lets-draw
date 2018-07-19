<template>
<b-container>
  <b-row>
    <b-col class="text-center">
      <canvas
        class="canvas"
        ref="canvas"
        @mousedown="penDown"
        @mousemove="penMove"
        @mouseup="penUp"
        @mouseleave="penUp">
      </canvas>
    </b-col>
  </b-row>
</b-container>
</template>

<script>
export default {
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
  },
  destroyed () {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    penDown (event) {
      this.contact = true
      this.ctx.moveTo(this.prevX, this.prevY)
    },
    penMove (event) {
      this.updateCoords(event)
      if (this.contact) {
        this.ctx.lineTo(this.currX, this.currY)
        this.ctx.stroke()
      }
    },
    penUp (event) {
      this.contact = false
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
