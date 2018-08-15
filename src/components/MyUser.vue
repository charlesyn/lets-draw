<template>
  <v-toolbar flat>
    <v-list>
      <v-list-tile avatar>
        <v-list-tile-avatar>
          <v-icon large>account_circle</v-icon>
        </v-list-tile-avatar>
          <v-text-field
            v-model='username'
            disabled
            >
          </v-text-field>
      </v-list-tile>
    </v-list>
  </v-toolbar>
</template>
<script>

export default {
  props: ['username'],
  name: 'MyUser',
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
<style scoped>

</style>
