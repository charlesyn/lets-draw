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
          <v-icon>face</v-icon>
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
  props: ['socket'],
  name: 'ServerUser',
  data () {
    return {
      Users: [
      ]
    }
  },
  mounted () {
  },
  methods: {
    hover () {
    }
  }
}
</script>

<style>

</style>
