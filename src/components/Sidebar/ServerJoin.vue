<template>
  <v-flex>
    <v-text-field
      placeholder='My Room'
      hint="Enter a room name to join a room"
      v-model='room'
      @keyup.enter='joinServer'
      >
    </v-text-field>
    <v-dialog
      v-model="dialog"
      hide-overlay
      persistent
      width="300">
      <v-card
        color="primary"
        dark>
        <v-card-text>
          Joining Room...
          <v-progress-linear
            indeterminate
            color="white"
            class="mb-0">
          </v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>
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
      room: '',
      dialog: false
    }
  },
  watch: {
    dialog (val) {
      if (!val) {
        return
      }
      setTimeout(() => (this.dialog = false), 2000)
    }
  },
  methods: {
    joinServer () {
      this.dialog = true
      this.socket.emit('room', { room: this.room, username: this.username })
    }
  }
}

</script>

<style scoped>

</style>
