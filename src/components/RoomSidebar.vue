<template>
  <v-navigation-drawer permanent absolute dark>
    <v-toolbar flat>
      <server-join :socket='socket'/>
    </v-toolbar>
  </v-navigation-drawer>
</template>
<script>
import ServerJoin from './ServerJoin'

export default {
  props: ['socket'],
  components: {
    ServerJoin
  },
  name: 'RoomSidebar',
  data () {
    return {
    }
  }
}
</script>
<style scoped>

</style>
