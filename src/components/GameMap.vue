<template>
  <div v-if="!win_state && !dead" class="map">
    <map-row :tiles="row1" :selectTile="selectTile" :selectedTile="selectedTile" />
    <map-row :tiles="row2" :selectTile="selectTile" :selectedTile="selectedTile" />
    <map-row :tiles="row3" :selectTile="selectTile" :selectedTile="selectedTile" />
  </div>
</template>

<script>
import MapRow from './MapRow'
import tiles from '../lib/tiles'

export default {
  name: 'game-map',
  components: {
    MapRow
  },
  props: ['win_state', 'dead', 'selectTile', 'selectedTile'],
  data () {
    const gameTiles = tiles.slice().sort(t => {
      return Math.floor(Math.random() * 3) >= 1 ? 1 : -1
    })
    return {
      row1: [gameTiles[0], gameTiles[1], gameTiles[2]],
      row2: [gameTiles[3], gameTiles[4], gameTiles[5]],
      row3: [gameTiles[6], gameTiles[7], gameTiles[8]]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}
</style>
