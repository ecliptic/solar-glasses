<template>
  <div :class="aspectRatio > 1 ? 'tileLandscape' : 'tilePortrait'" @click="select()">
    <div
      v-if="tile.type === 'grass'"
      :class="{desaturate: tile.walked, icon: true, grass: true}"
      style="background-image: url('static/icons/grass.png'); background-size: cover;"
    >
      <img
        v-if="hasPlayer"
        class="player"
        src="static/icons/player.png"
      />
    </div>
    <div
      v-else
      :class="{desaturate: tile.walked, icon: true, tree: true}"
      style="background-image: url('static/icons/tree.png'); background-size: cover;"
    >
      <img
        v-if="hasPlayer"
        class="player"
        src="static/icons/player.png"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'map-tile',
  props: [
    'tile',
    'hasPlayer',
    'selectTile',
    'aspectRatio'
  ],
  methods: {
    select () {
      console.log(this.tile)
      this.selectTile(this.tile)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tilePortrait {
  width: 25vw;
  max-width: 12.5vh;
  height: 25vw;
  max-height: 12.5vh;
  cursor: pointer;
}

.tileLandscape {
  width: 25vh;
  max-width: 12.5vw;
  height: 25vh;
  max-height: 12.5vw;
  cursor: pointer;
}

.icon {
  width: 100%;
  height: 100%;
}

.grass {
  background: green;
}

.tree {
  background: brown;
}

.player {
  width: 100%;
  height: 100%;
}

.desaturate {
  filter: grayscale(1);
}
</style>
