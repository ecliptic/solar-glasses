<template>
  <div id="main" :style="{height: viewportHeight}">
    <game-dashboard
      :selectedTile="selectedTile"
      :live_message="live_message"
      :win_state="win_state"
      :dead="dead"
      :gameStart="gameStart"
      :aspectRatio="aspectRatio"
      :viewportHeight="viewportHeight"
      :turnsLeft="turnsLeft"
      :playAgain="playAgain"
    />
    <game-map
      v-if="!win_state && !dead"
      :selectTile="selectTile"
      :selectedTile="selectedTile"
      :aspectRatio="aspectRatio"
      :viewportHeight="viewportHeight"
      :char="char"
    />
    <div
      v-if="message"
      class="message"
    >
      <h1 v-if="message.prompt">{{message.prompt}}</h1>
      <p v-if="message.body">{{message.body}}</p>
      <p v-if="gameStart">Choose a character:</p>
      <span class="options" v-if="message.options">
        <button
          class="option"
          v-if="message.options.one"
          @click="checkOption(selectedOptions[0])"
        >
          {{message.options.one}}
        </button>
        <img
          v-if="gameStart"
          class="chars"
          src="/static/images/char1.png"
          @click="chooseChar(1)"
        />
        <button
          class="option"
          v-if="message.options.two"
          @click="checkOption(selectedOptions[1])"
        >
          {{message.options.two}}
        </button>
        <button
          class="option"
          v-if="message.options.three"
          @click="clearMessage"
        >
          {{message.options.three}}
        </button>
        <img
          v-if="gameStart"
          class="chars"
          src="/static/images/char2.png"
          @click="chooseChar(2)"
        />
      </span>
    </div>
    <div class="message" v-if="dead">
      <h1>You missed the eclipse. Better luck in 7 years.</h1>
      <span class="options">
        <button
          class="option"
          @click="playAgain()"
        >
          Play again
        </button>
      </span>
    </div>
  </div>
</template>

<script>
import GameDashboard from './GameDashboard.vue'
import GameMap from './GameMap'

const viewportWidth = () => document.documentElement.clientWidth
const viewportHeight = () => window.innerHeight

/* eslint-disable max-len */
export default {
  name: 'main',
  components: {
    GameDashboard,
    GameMap,
  },
  beforeMount() {
    document.body.style.height = viewportHeight()
  },
  data() {
    return {
      char: undefined,
      turnsLeft: 16,
      message: {
        prompt: 'The date is August 21st, 2017. The time is 11:30, Mountain Time.',
        body: 'You procrastinated getting your solar glasses, and now you have 15 minutes to get some.',
        options: 'choose',
      },
      selectedTile: {},
      selectedOptions: [],
      live_message: '',
      dead: false,
      win_state: false,
      aspectRatio: viewportWidth() / viewportHeight(),
      viewportHeight: `${viewportHeight()}px`,
    }
  },
  computed: {
    gameStart() {
      return this.turnsLeft === 16
    },
  },
  mounted() {
    window.addEventListener('resize', this.checkAspectRatio)
  },
  beforeUpdate() {
    if (this.turnsLeft < 0) {
      this.turnsLeft = 0
    }
  },
  destroyed() {
    window.removeEventListener('resize', this.checkAspectRatio)
  },
  methods: {
    checkAspectRatio() {
      this.aspectRatio = viewportWidth() / viewportHeight()
      this.viewportHeight = `${viewportHeight()}px`
      document.body.style.height = viewportHeight()
    },
    chooseChar(num) {
      this.char = num
      this.turnsLeft -= 1
      this.message = false
    },
    selectTile(tile) {
      if (!tile.walked && (this.turnsLeft === 15 || this.selectedTile)) {
        this.$set(tile, 'walked', true)
        this.selectedTile = tile
        this.turnsLeft -= 1
        this.selectedOptions = Math.floor(Math.random() * 3) >= 1
          ? [tile.live_option, tile.death_option]
          : [tile.death_option, tile.live_option]
        this.message = {
          prompt: tile.prompt,
          body: 'What do you do?',
          options: {
            one: this.selectedOptions[0],
            two: this.selectedOptions[1],
          },
        }
      }
    },
    checkOption(option) {
      if (option === this.selectedTile.death_option) {
        this.message = {
          body: this.selectedTile.death_message,
          options: {
            three: 'Click to continue',
          },
        }
        this.turnsLeft -= this.selectedTile.consequence
      }
      else {
        this.message = {
          body: this.selectedTile.live_message,
          options: {
            three: 'Click to continue',
          },
        }
        if (this.selectedTile.win_state) {
          this.win_state = true
        }
      }
    },
    clearMessage() {
      if (this.turnsLeft <= 0 && !this.win_state) {
        this.dead = true
      }
      if (this.win_state) {
        this.turnsLeft = 0
      }
      this.message = undefined
    },
    playAgain() {
      window.location.reload()
    },
    nextTurn() {
      this.turnsLeft -= 1
      this.message = false
    },
  },
}
/* eslint-enable max-len */
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: gray;
}

h1 {
  font-size: 1.5em;
}

#main {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding: 0;
  margin: 0;
  overflow: hidden;
  font-family: 'Press Start 2P', courier, sans-serif;
  color: white;
}

.message {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: absolute;
  width: calc(100% - 30px);
  height: calc(100% - 30px);
  padding: 30px;
  background: black;
  text-align: center;
  z-index: 20;
}

.options {
  width: 90%;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: center;
}

.option {
  width: 45%;
  margin-top: 16px;
  padding: 8px;
  background-color: white;
  border: 0;
  border-radius: 2px;
  cursor: pointer;
  font-family: 'Press Start 2P', courier, sans-serif;
}

.option:hover {
  background-color: lightgray;
}

.chars {
  width: calc(5vw + 5vh);
  height: calc(5vw + 5vh);
  cursor: pointer;
}
</style>
