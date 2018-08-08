<template>
  <v-toolbar flat>
    <v-list>
      <v-list-tile avatar>
        <v-list-tile-avatar>
        </v-list-tile-avatar>
        <v-list-tile-content>
          <v-text-field
            placeholder='Me'
            hint='Username'
            v-model='username'
            @keyup.enter='setUser'
            >
          </v-text-field>
        </v-list-tile-content>
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
