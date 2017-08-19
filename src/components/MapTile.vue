<template>
  <div
    @click="select()"
    :class="{
      tilePortrait: aspectRatio <= 1,
      tileLandscape: aspectRatio > 1,
      desaturate: tile.walked,
      grass: type === 'grass',
      tree: type === 'tree',
    }"
  >
    <img
      v-if="hasPlayer"
      class="player"
      src="../assets/icons/player.png"
    />
  </div>
</template>

<script>
export default {
  name: 'map-tile',
  props: [
    'tile',
    'hasPlayer',
    'selectTile',
    'aspectRatio',
  ],
  data() {
    function getRandom(minNum, maxNum) {
      const min = Math.ceil(minNum)
      const max = Math.floor(maxNum)
      return Math.floor(Math.random() * (max - min + 1)) + min
    }
    return {
      type: getRandom(0, 1) > 0 ? 'grass' : 'tree',
    }
  },
  methods: {
    select() {
      console.log(this.tile)
      this.selectTile(this.tile)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tilePortrait {
  width: calc(25vw - 9px);
  max-width: calc(12.5vh - 4.5px);
  height: calc(25vw - 9px);
  max-height: calc(12.5vh - 4.5px);
  cursor: pointer;
}

.tileLandscape {
  width: calc(25vh - 9px);
  max-width: calc(12.5vw - 4.5px);
  height: calc(25vh - 9px);
  max-height: calc(12.5vw - 4.5px);
  cursor: pointer;
}

.grass {
  background: green;
  background-image: url('../assets/icons/grass.png');
  background-size: cover;
}

.tree {
  background: brown;
  background-image: url('../assets/icons/tree.png');
  background-size: cover;
}

.player {
  width: 100%;
  height: 100%;
}

.desaturate {
  filter: grayscale(1);
}
</style>
