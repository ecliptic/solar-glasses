<template>
  <div
    @click="select()"
    :class="{
      tileBase: true,
      desaturate: tile.walked,
    }"
    :style="{
      height: aspectRatio > 1 ? `calc(${viewportHeight} / 4)` : '25vw',
      maxHeight: aspectRatio > 1 ? '12.5vw' : `calc(${viewportHeight} / 8)`,
      width: aspectRatio > 1 ? `calc(${viewportHeight} / 4)` : '25vw',
      maxWidth: aspectRatio > 1 ? '12.5vw' : `calc(${viewportHeight} / 8)`,
    }"
  >
    <div
      v-if="tile.type"
      :class="{
        icon: true,
        desaturate: tile.walked,
      }"
      :style="{backgroundImage: `url(/static/images/${tile.type}.png)`}"
    >
      <div
        v-if="hasPlayer && !tile.type.includes('road')"
        class="player"
        :style="{backgroundImage: `url(/static/images/char${char}.png)`}"
      />
      <div
        v-if="hasPlayer && tile.type.includes('road')"
        class="player"
        :style="{backgroundImage: `url(/static/images/carRight.png)`}"
      />
    </div>
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
    'viewportHeight',
    'char',
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
  mix-blend-mode: hard-light;
}

.icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}

.player {
  width: 75%;
  height: 75%;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}

.desaturate {
  background-color: rgba(0, 0, 0, 0.5);
  background-blend-mode: darken;
}
</style>
