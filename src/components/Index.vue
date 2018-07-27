<template>
  <div>
    <server-join/>
    <canvas-vue/>
  </div>
</template>

<script>
import CanvasVue from './Canvas'
import ServerJoin from './ServerJoin'

export default {
  components: {
    CanvasVue,
    ServerJoin
  },
  name: 'Index',
  data () {
    return {
    }
  }
}
</script>

<style scoped>

</style>
