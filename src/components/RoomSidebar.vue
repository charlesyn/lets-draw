<template>
  <v-navigation-drawer permanent absolute>
    <v-toolbar flat>
      <server-join :socket='socket' :username='username'/>
    </v-toolbar>
    <server-users/>
    <myUser id='myUser' v-on:setUser='updateUser($event)' />
  </v-navigation-drawer>
</template>
<script>
import ServerJoin from './ServerJoin'
import ServerUsers from './ServerUsers'
import MyUser from './MyUser'

export default {
  props: ['socket'],
  components: {
    ServerJoin,
    ServerUsers,
    MyUser
  },
  name: 'RoomSidebar',
  data () {
    return {
      username: ''
    }
  },
  methods: {
    updateUser (username) {
      this.username = username
      console.log(username)
    }
  }
}
</script>
<style scoped>
  #myUser {
    position: absolute;
    bottom: 0;
  }
</style>
