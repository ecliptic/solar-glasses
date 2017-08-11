<template>
  <div>
    <div v-if="!dead" class="map">
      <div class="buttonContainer">
        <p class="title">{{selectedTile.prompt}}</p>
        <p class="button" @click="checkOption(selectedOptions[0])">{{selectedOptions[0]}}</p>
        <p class="button" @click="checkOption(selectedOptions[1])">{{selectedOptions[1]}}</p>
      </div>
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
      row1: [gameTiles[0], gameTiles[1], gameTiles[2]],
      row2: [gameTiles[3], gameTiles[4], gameTiles[5]],
      row3: [gameTiles[6], gameTiles[7], gameTiles[8]],
      selectedTile: {},
      selectedOptions: [],
      dead: false
    }
  },
  methods: {
    selectTile (tile) {
      this.selectedTile = tile
      this.selectedOptions = Math.floor(Math.random() * 3) >= 1 ? [this.selectedTile.live_option, this.selectedTile.death_option] : [this.selectedTile.death_option, this.selectedTile.live_option]
    },
    checkOption (option) {
      if (option === this.selectedTile.death_option) {
        this.dead = true
      } else {
        alert('live')
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

.buttonContainer {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.title {
  width: 50%;
}

.button {
  width: 50%;
  border: 1px solid black;
  cursor: pointer;
}

.button:hover {
  background-color: black;
  color: white;
}
</style>
