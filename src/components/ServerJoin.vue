<template>
  <v-container>
    <v-layout>
      <v-flex md4 offset-md4>
        <v-text-field
          label='Room'
          placeholder='Join a Room'
          v-model='room'
          @keyup.enter='joinServer'
          >
        </v-text-field>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import io from 'socket.io-client'
export default {
  name: 'ServerJoin',
  mounted () {
    this.socket = io('localhost:8081')
  },
  data () {
    return {
      room: '',
      socket: null
    }
  },
  methods: {
    joinServer () {
      this.socket.emit('room', this.room)
    }
  }
}

</script>

<style scoped>

</style>
