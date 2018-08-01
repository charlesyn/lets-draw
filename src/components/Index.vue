<template>
  <div>
    <server-join :socket='socket'/>
    <canvas-vue :socket='socket'/>
  </div>
</template>

<script>
import io from 'socket.io-client'
import CanvasVue from './Canvas'
import ServerJoin from './ServerJoin'

export default {
  components: {
    CanvasVue,
    ServerJoin
  },
  name: 'Index',
  created () {
    this.socket = io('localhost:8081')
  },
  mounted () {
  },
  data () {
    return {
      socket: null
    }
  }
}
</script>

<style scoped>

</style>
