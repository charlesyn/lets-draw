<template>
  <div>
    <link href='https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons' rel="stylesheet" type="text/css">
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
