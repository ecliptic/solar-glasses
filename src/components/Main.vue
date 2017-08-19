<template>
  <div id="main">
    <game-dashboard
      :selectedTile="selectedTile"
      :live_message="live_message"
      :win_state="win_state"
      :dead="dead"
      :gameStart="gameStart"
      :aspectRatio="aspectRatio"
    />
    <game-map
      v-if="!win_state && !dead"
      :selectTile="selectTile"
      :selectedTile="selectedTile"
      :aspectRatio="aspectRatio"
    />
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
import GameDashboard from './GameDashboard.vue'
import GameMap from './GameMap'

const viewportWidth = () => document.documentElement.clientWidth
const viewportHeight = () => document.documentElement.clientHeight

export default {
  name: 'main',
  components: {
    GameDashboard,
    GameMap,
  },
  data() {
    return {
      gameStart: true,
      selectedTile: {},
      selectedOptions: [],
      live_message: '',
      dead: false,
      win_state: false,
      aspectRatio: viewportWidth() / viewportHeight(),
    }
  },
  mounted() {
    window.addEventListener('resize', this.checkAspectRatio)
  },
  destroyed() {
    window.removeEventListener('resize', this.checkAspectRatio)
  },
  methods: {
    checkAspectRatio() {
      this.aspectRatio = viewportWidth() / viewportHeight()
    },
    selectTile(tile) {
      if (!tile.walked && (this.gameStart || (this.selectedTile && this.live_message))) {
        this.gameStart = false
        this.live_message = ''
        this.selectedTile = tile
        this.selectedOptions = Math.floor(Math.random() * 3) >= 1
          ? [this.selectedTile.live_option, this.selectedTile.death_option]
          : [this.selectedTile.death_option, this.selectedTile.live_option]
      }
    },
    playAgain() {
      window.location.reload()
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#main {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: calc(100vw - 36px);
  height: calc(100vh - 36px);
  padding: 18px;
}
</style>
