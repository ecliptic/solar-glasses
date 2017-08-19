<template>
  <div :id="aspectRatio > 1 ? 'dashboardLandscape' : 'dashboardPortrait'">
    <div v-if="!win_state && !gameStart && !dead && !live_message" id="buttonContainer">
      <h2 class="title">{{selectedTile.prompt}}</h2>
      <p class="button" @click="checkOption(selectedOptions[0])">{{selectedOptions[0]}}</p>
      <p class="button" @click="checkOption(selectedOptions[1])">{{selectedOptions[1]}}</p>
    </div>
    <div v-if="!win_state && live_message && !dead">
      <h2>{{live_message}}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: 'game-dashboard',
  props: ['selectedTile', 'live_message', 'win_state', 'dead', 'gameStart', 'aspectRatio'],
  methods: {
    checkOption(option) {
      if (option === this.selectedTile.death_option) {
        this.dead = true
      }
      else {
        this.live_message = this.selectedTile.live_message
        this.$set(this.selectedTile, 'walked', true)
        if (this.selectedTile.win_state) {
          this.win_state = true
        }
      }
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title {
  width: 500px;
}

#buttonContainer {
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

#dashboardPortrait {
  width: calc(100vw - 36px);
  height: calc(50vh - 18px);
  overflow: hidden;
}

#dashboardLandscape {
  width: calc(50vw - 18px);
  height: calc(100vh - 36px);
  overflow: hidden;
}
</style>
