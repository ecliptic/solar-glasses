<template>
  <center>
    <h1 v-if="gameStart">Click a tile to Play.</h1>
    <div v-if="!win_state && !gameStart && !dead && !live_message" class="buttonContainer">
      <h1 class="title">{{selectedTile.prompt}}</h1>
      <p class="button" @click="checkOption(selectedOptions[0])">{{selectedOptions[0]}}</p>
      <p class="button" @click="checkOption(selectedOptions[1])">{{selectedOptions[1]}}</p>
    </div>
    <div v-if="!win_state && live_message && !dead">
      <h2>{{live_message}}</h2>
    </div>
    <div v-if="!win_state && !dead" class="map">
      <Tile v-for="tile in row1" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
      <Tile v-for="tile in row2" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
      <Tile v-for="tile in row3" :key="tile.prompt" :tile="tile" :selectTile="selectTile" :hasPlayer="selectedTile === tile" />
    </div>
    <div v-if="!win_state && dead">
      <h1>{{selectedTile.death_message}}</h1>
      <h2>You died</h2>
      <p class="button" @click="playAgain()">Play Again</p>
    </div>
    <div v-if="win_state">
      <h1>🎉 Congratulations. You are one with nature.</h1>
      <p class="button" @click="playAgain()">Play Again</p>
    </div>
  </center>
</template>

<script>
import Tile from './Tile'
import tiles from '../lib/tiles'

const gameTiles = tiles.slice().sort(t => {
  return Math.floor(Math.random() * 3) >= 1 ? 1 : -1
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
      live_message: '',
      win_state: false
    }
  },
  methods: {
    selectTile (tile) {
      if (!tile.walked && (this.gameStart || this.selectedTile && this.live_message)) {
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
        if (this.selectedTile.win_state) {
          this.win_state = true
        }
      }
    },
    playAgain () {
      window.location.reload()
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
