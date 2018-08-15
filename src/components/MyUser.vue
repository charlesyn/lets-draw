<template>
  <v-toolbar flat>
    <v-list>
      <v-list-tile avatar>
        <v-list-tile-avatar>
          <v-icon large>account_circle</v-icon>
        </v-list-tile-avatar>
          <v-text-field
            placeholder='Me'
            hint='Username'
            v-model='username'
            @keyup.enter='setUser'
            >
          </v-text-field>
      </v-list-tile>
    </v-list>
  </v-toolbar>
</template>
<script>

export default {
  name: 'MyUser',
  data () {
    return {
      username: ''
    }
  },
  methods: {
    setUser () {
      this.$emit('setUser', this.username)
    }
  }
}
</script>
<style scoped>

</style>
