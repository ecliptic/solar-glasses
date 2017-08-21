<template>
  <div
    class="dashboard"
    :style="{
      width: width,
      height: height,
      backgroundImage: `${this.turn < 0 ? 'url(/static/images/turn0.png' : `url(/static/images/turn${turn}.png)`}`
    }"
  >
    <div
      id="sun"
      :style="{
        height: aspectRatio > 1 ? `calc(${viewportHeight} / 1.9)` : '51vw',
        maxHeight: aspectRatio > 1 ? '25.5vw' : `calc(${viewportHeight} / 3.9)`,
        width: aspectRatio > 1 ? `calc(${viewportHeight} / 1.9)` : '51vw',
        maxWidth: aspectRatio > 1 ? '25.5vw' : `calc(${viewportHeight} / 3.9)`,
        filter: `blur(calc(${turnsLeft}px + 1px))`,
        boxShadow: `0 0 calc(${turnsLeft}vw + ${turnsLeft}vh) calc(${turnsLeft / 2}vw + ${turnsLeft / 2}vh) white`,
      }"
    >
      <div
        id="moon"
        :style="{
          height: aspectRatio > 1 ? `calc(${viewportHeight} / 2.05)` : '49vw',
          maxHeight: aspectRatio > 1 ? '24.5vw' : `calc(${viewportHeight} / 4.05)`,
          width: aspectRatio > 1 ? `calc(${viewportHeight} / 2.05)` : '49vw',
          maxWidth: aspectRatio > 1 ? '24.5vw' : `calc(${viewportHeight} / 4.05)`,
          marginLeft: `calc(${turnsLeft}vw + ${turnsLeft}vh + 0.25vw + 0.25vh)`,
          marginTop: `calc(${turnsLeft * -1}vw + ${turnsLeft * -1}vh + 0.25vw + 0.25vh)`,
        }"
      />
    </div>
    <div v-if="turnsLeft > 0" class="dashMessage">
      <span>{{turnsLeft}} minute{{turnsLeft === 1 ? '' : 's'}} left<br></br>{{gameStartMessage}}</span>
    </div>
    <div v-if="turnsLeft <= 0" class="dashMessage">
      You got eclipse glasses just in time, you cool cat. 😎
    </div>
    <span v-if="turnsLeft <= 0" class="options">
      <button
        class="option"
        @click="playAgain()"
      >
        Play again
      </button>
    </span>
  </div>
</template>

<script>
export default {
  name: 'game-dashboard',
  props: [
    'aspectRatio',
    'viewportHeight',
    'turnsLeft',
    'playAgain',
  ],
  computed: {
    width() {
      if (this.turnsLeft <= 0 || this.aspectRatio <= 1) {
        return '100vw'
      }
      return '50vw'
    },
    height() {
      if (this.turnsLeft <= 0 || this.aspectRatio > 1) {
        return this.viewportHeight
      }
      return `calc(${this.viewportHeight} / 2)`
    },
    turn() {
      return 16 - this.turnsLeft
    },
    gameStartMessage() {
      if (this.turnsLeft === 15) {
        return 'Click anywhere on the map to begin. Each click uses up 1 minute.'
      }
      return undefined
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
span {
  font-size: 1em;
}

.dashboard {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  overflow: hidden;
  background-image: url('/static/images/turn1.png');
  background-size: cover;
}

#sun {
  border-radius: 50%;
  background: white;
}

#moon {
  border-radius: 50%;
  background: black;
}

#buttonContainer {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.dashMessage {
  padding: 30px;
  text-align: center;
  text-shadow: 2px 2px 0 black;
  z-index: 10;
}
</style>
