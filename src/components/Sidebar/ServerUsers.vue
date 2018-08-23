<template>
  <v-list dense>
    <v-list-group prepend-icon='account_circle' value='true'>
      <v-list-tile slot='activator'>
        <v-list-tile-title>Users Online</v-list-tile-title>
      </v-list-tile>
      <v-list-tile
        v-for='User in Users'
        :key='User.name'
        avatar
        @click='hover'>
        <v-list-tile-avatar>
          <v-icon>person</v-icon>
        </v-list-tile-avatar>
        <v-list-tile-content>
          <v-list-tile-title v-text='User.name'></v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>
    </v-list-group>
  </v-list>
</template>

<script>
export default {
  props: ['socket', 'username'],
  name: 'ServerUser',
  data () {
    return {
      Users: [
      ]
    }
  },
  mounted () {
    this.socket.on('pollUsers', this.sendUsername)
    this.socket.on('removeUser', this.removeUserFromList)
    this.socket.on('clearUserList', this.clearUserList)
    this.socket.on('updateUserList', this.updateUserList)
  },
  methods: {
    hover () {
    },
    sendUsername (data) {
      this.socket.emit('getUserList', {
        username: this.username,
        recipient: data
      })
    },
    updateUserList (data) {
      console.log(data)
      this.Users.push({ name: data })
    },
    removeUserFromList (data) {
      this.Users.splice(this.Users.findIndex(item => item.name === data), 1)
    },
    clearUserList () {
      this.Users = []
    }
  }
}
</script>

<style>

</style>
