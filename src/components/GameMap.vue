<template>
  <div class="map">
    <Tile v-for="tile in row1" :key="tile.prompt" :tile="tile" :selectTile="selectTile" />
    <Tile v-for="tile in row2" :key="tile.prompt" :tile="tile" :selectTile="selectTile" />
    <Tile v-for="tile in row3" :key="tile.prompt" :tile="tile" :selectTile="selectTile" />
  </div>
</template>

<script>
import Tile from './Tile'
import tiles from '../lib/tiles'

const gameTiles = tiles.slice().sort(t => {
  return Math.floor(Math.random() * 2) > 1 ? 1 : -1
})

export default {
  name: 'GameMap',
  components: {
    Tile
  },
  data () {
    return {
      row1: [gameTiles[0], gameTiles[1], gameTiles[2]],
      row2: [gameTiles[3], gameTiles[4], gameTiles[5]],
      row3: [gameTiles[6], gameTiles[7], gameTiles[8]],
      selectedTile: {}
    }
  },
  methods: {
    selectTile (tile) {
      console.log(tile)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  width: 100vh;
  height: 100vh;
}
</style>
