<template>
  <div>
    <map-tile :aspectRatio="aspectRatio" v-for="tile in tiles" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
  </div>
</template>

<script>
import MapTile from './MapTile'

export default {
  name: 'map-row',
  components: {
    MapTile
  },
  props: ['tiles', 'selectTile', 'selectedTile', 'aspectRatio']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  display: flex;
  flex-wrap: nowrap;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}
</style>
