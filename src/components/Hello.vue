<template>
  <Map />
</template>

<script>
import Map from './Map'
export default {
  name: 'hello',
  components: {
    Map,
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  width: 100vw;
  height: 100vh;
}
</style>
