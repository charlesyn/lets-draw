<template>
  <div>
    <set-user v-on:usernameSet='setUsername($event)'/>
    <room-sidebar :socket='socket' :username='username'/>
    <v-layout>
      <canvas-vue :socket='socket'/>
    </v-layout>
  </div>
</template>

<script>
import io from 'socket.io-client'
import CanvasVue from './Drawing/Canvas'
import RoomSidebar from './Sidebar/RoomSidebar'
import SetUser from './SetUser'

export default {
  components: {
    RoomSidebar,
    CanvasVue,
    SetUser
  },
  name: 'Index',
  created () {
    this.socket = io('localhost:8081')
  },
  mounted () {
  },
  data () {
    return {
      socket: null,
      username: ''
    }
  },
  methods: {
    setUsername (data) {
      this.username = data
      console.log(data)
    }
  }
}
</script>

<style scoped>
</style>
