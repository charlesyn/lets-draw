<template>
  <v-flex>
    <v-text-field
      placeholder='My Room'
      hint="Enter a room name to join a room"
      v-model='room'
      @keyup.enter='joinServer'
      >
    </v-text-field>
  </v-flex>
</template>

<script>
export default {
  props: ['socket', 'username'],
  name: 'ServerJoin',
  mounted () {
  },
  data () {
    return {
      room: ''
    }
  },
  methods: {
    joinServer () {
      this.socket.emit('room', { room: this.room, username: this.username })
    }
  }
}

</script>

<style scoped>

</style>
