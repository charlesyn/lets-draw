<template>
  <div>
    <room-sidebar :socket='socket'/>
    <v-layout>
      <canvas-vue :socket='socket'/>
    </v-layout>
  </div>
</template>

<script>
import io from 'socket.io-client'
import CanvasVue from './Canvas'
import RoomSidebar from './RoomSidebar'

export default {
  components: {
    RoomSidebar,
    CanvasVue
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
