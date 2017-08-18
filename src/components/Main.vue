<template>
  <div>
    <h1 class="title-logo">Stay Unplugged</h1>
    <h1 v-if="gameStart">Click a tile to Play.</h1>
    <div v-if="!win_state && !gameStart && !dead && !live_message" class="buttonContainer">
      <h2 class="title">{{selectedTile.prompt}}</h2>
      <p class="button" @click="checkOption(selectedOptions[0])">{{selectedOptions[0]}}</p>
      <p class="button" @click="checkOption(selectedOptions[1])">{{selectedOptions[1]}}</p>
    </div>
    <div v-if="!win_state && live_message && !dead">
      <h2>{{live_message}}</h2>
    </div>
    <game-map :win_state="win_state" :dead="dead" :selectTile="selectTile" :selectedTile="selectedTile" />
    <div v-if="!win_state && dead">
      <h1>{{selectedTile.death_message}}</h1>
      <h2>You died</h2>
      <p class="button" @click="playAgain()">Play Again</p>
    </div>
    <div v-if="win_state">
      <h1>🎉 Congratulations. You are one with nature.</h1>
      <p class="button" @click="playAgain()">Play Again</p>
    </div>
  </div>
</template>

<script>
import GameMap from './GameMap'
export default {
  name: 'main',
  components: {
    GameMap
  },
  data () {
    return {
      gameStart: true,
      selectedTile: {},
      selectedOptions: [],
      live_message: '',
      dead: false,
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
.title-logo {
  font-size: 2em;
  color: green;
  font-family: 'Walter Turncoat';
}

.title {
  width: 500px;
}

.buttonContainer {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
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
