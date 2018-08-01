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
export default {
  props: ['socket'],
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
      this.socket.emit('room', this.room)
    }
  }
}

</script>

<style scoped>

</style>
