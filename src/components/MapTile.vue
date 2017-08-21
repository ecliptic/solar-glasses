<template>
  <div
    @click="select()"
    :class="{
      tileBase: true,
      tilePortrait: aspectRatio <= 1,
      tileLandscape: aspectRatio > 1,
      desaturate: tile.walked,
    }"
  >
    <div
      v-if="tile.type"
      class="icon"
      :style="{backgroundImage: `url(/static/images/${tile.type}.png)`}"
    />
  </div>
</template>

<script>
import {getRandom} from '../lib/utils'

export default {
  name: 'map-tile',
  props: [
    'tile',
    'hasPlayer',
    'selectTile',
    'aspectRatio',
  ],
  methods: {
    select() {
      this.selectTile(this.tile)
    },
  },
  beforeMount() {
    if (!this.tile.type) {
      const randomNum = getRandom(1, 4)
      switch (randomNum) {
        case 1: this.tile.type = 'apartment'
          break
        case 2: this.tile.type = 'shop'
          break
        case 3: this.tile.type = 'office'
          break
        case 4: this.tile.type = 'store'
          break
        case 5: this.tile.type = 'house'
          break
        default: this.tile.type = 'apartment'
          break
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tileBase {
  background-image: url('/static/images/roadPLAZA.png');
  background-size: contain;
  cursor: pointer;
}

.tilePortrait {
  width: calc(25vw - 9px);
  max-width: calc(12.5vh - 4.5px);
  height: calc(25vw - 9px);
  max-height: calc(12.5vh - 4.5px);
}

.tileLandscape {
  width: calc(25vh - 9px);
  max-width: calc(12.5vw - 4.5px);
  height: calc(25vh - 9px);
  max-height: calc(12.5vw - 4.5px);
}

.icon {
  width: 100%;
  height: 100%;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}

.desaturate {
  filter: grayscale(1);
}
</style>
