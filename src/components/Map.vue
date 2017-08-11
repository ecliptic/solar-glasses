<template>
  <div class="map">
    <Tile v-for="tile in row1" />
    <Tile v-for="tile in row2" />
    <Tile v-for="tile in row3" />
  </div>
</template>

<script>
import Tile from './Tile'
export default {
  name: 'Map',
  components: {
    Tile,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {

}
</style>
