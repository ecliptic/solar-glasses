<template>
  <div>
    <h1 class="title-logo">Stay Unplugged</h1>
    <GameMap />
  </div>
</template>

<script>
import GameMap from './GameMap'
export default {
  name: 'hello',
  components: {
    GameMap
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
.title-logo {
  font-size: 2em;
  color: green;
  font-family: 'Walter Turncoat';
}
</style>
