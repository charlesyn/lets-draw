<template>
  <v-layout row justify center>
    <v-dialog v-model='dialog' persistent max-width='500'>
      <v-card>
        <v-card-title class='headline'>Select Username</v-card-title>
        <v-card-actions>
          <v-text-field
            v-model='username'
            @keyup.enter='setInformation'
            >
          </v-text-field>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
export default {
  name: 'SetUser',
  data () {
    return {
      dialog: true,
      username: ''
    }
  },
  methods: {
    setInformation () {
      this.$emit('usernameSet', this.username)
      this.dialog = false
    }
  }
}
</script>
<style scoped>

</style>
