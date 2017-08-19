<template>
  <div :id="aspectRatio > 1 ? 'mapLandscape' : 'mapPortrait'">
    <map-row :aspectRatio="aspectRatio" :tiles="row1" :selectTile="selectTile" :selectedTile="selectedTile" />
    <map-row :aspectRatio="aspectRatio" :tiles="row2" :selectTile="selectTile" :selectedTile="selectedTile" />
    <map-row :aspectRatio="aspectRatio" :tiles="row3" :selectTile="selectTile" :selectedTile="selectedTile" />
    <map-row :aspectRatio="aspectRatio" :tiles="row4" :selectTile="selectTile" :selectedTile="selectedTile" />
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
  props: ['selectTile', 'selectedTile', 'aspectRatio'],
  data () {
    const gameTiles = tiles.slice().sort(t => {
      return Math.floor(Math.random() * 3) >= 1 ? 1 : -1
    })
    return {
      row1: [gameTiles[0], gameTiles[1], gameTiles[2], gameTiles[3]],
      row2: [gameTiles[4], gameTiles[5], gameTiles[6], gameTiles[7]],
      row3: [gameTiles[8], gameTiles[9], gameTiles[10], gameTiles[11]],
      row4: [gameTiles[12], gameTiles[13], gameTiles[14], gameTiles[15]]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#mapPortrait {
  width: 100vw;
  height: 50vh;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

#mapLandscape {
  width: 50vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: center;
}
</style>
