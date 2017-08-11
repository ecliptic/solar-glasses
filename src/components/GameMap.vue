<template>
  <div>
    <div v-if="!dead && !live_message">
      <h1>{{selectedTile.prompt}}</h1>
      <p @click="checkOption(selectedOptions[0])">{{selectedOptions[0]}}</p>
      <p @click="checkOption(selectedOptions[1])">{{selectedOptions[1]}}</p>
    </div>
    <div v-if="live_message && !dead">
      <h2>{{live_message}}</h2>
    </div>
    <div v-if="!dead" class="map">
      <Tile v-for="tile in row1" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
      <Tile v-for="tile in row2" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
      <Tile v-for="tile in row3" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
    </div>
    <div v-if="dead">
      <h1>{{selectedTile.death_message}}</h1>
      <h2>You died</h2>
    </div>
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
      gameStart: true,
      row1: [gameTiles[0], gameTiles[1], gameTiles[2]],
      row2: [gameTiles[3], gameTiles[4], gameTiles[5]],
      row3: [gameTiles[6], gameTiles[7], gameTiles[8]],
      selectedTile: {},
      selectedOptions: [],
      dead: false,
      live_message: ''
    }
  },
  methods: {
    selectTile (tile) {
      if (this.gameStart || this.selectedTile && this.live_message) {
        this.gameStart = false
        this.live_message = ''
        this.selectedTile = tile
        this.selectedOptions = Math.floor(Math.random() * 3) >= 1 ? [this.selectedTile.live_option, this.selectedTile.death_option] : [this.selectedTile.death_option, this.selectedTile.live_option]
      }
    },
    checkOption (option) {
      if (option === this.selectedTile.death_option) {
        this.dead = true
      } else {
        this.live_message = this.selectedTile.live_message
        this.$set(this.selectedTile, 'walked', true)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  width: 90vh;
  height: 90vh;
  display: flex;
  flex-wrap: wrap;
}
</style>
