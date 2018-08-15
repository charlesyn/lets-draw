<template>
  <v-navigation-drawer permanent absolute>
    <v-toolbar flat>
      <server-join :socket='socket' :username='username'/>
    </v-toolbar>
    <server-users :socket='socket'/>
    <myUser id='myUser' :username='username' />
  </v-navigation-drawer>
</template>
<script>
import ServerJoin from './ServerJoin'
import ServerUsers from './ServerUsers'
import MyUser from './MyUser'

export default {
  props: ['socket', 'username'],
  components: {
    ServerJoin,
    ServerUsers,
    MyUser
  },
  name: 'RoomSidebar',
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
<style scoped>
  #myUser {
    position: absolute;
    bottom: 0;
  }
</style>
