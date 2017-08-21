<template>
  <div
    :class="{
      map: true,
      mapLandscape: aspectRatio > 1,
      mapPortrait: aspectRatio <= 1,
      show: !message,
      hide: message,
    }"
    :style="{
      height: aspectRatio > 1 ? viewportHeight : `calc(${viewportHeight} / 2)`,
    }"
  >
    <map-row
      :aspectRatio="aspectRatio"
      :tiles="configuration.row1"
      :selectTile="selectTile"
      :selectedTile="selectedTile"
      :viewportHeight="viewportHeight"
      :char="char"
    />
    <map-row
      :aspectRatio="aspectRatio"
      :tiles="configuration.row2"
      :selectTile="selectTile"
      :selectedTile="selectedTile"
      :viewportHeight="viewportHeight"
      :char="char"
    />
    <map-row
      :aspectRatio="aspectRatio"
      :tiles="configuration.row3"
      :selectTile="selectTile"
      :selectedTile="selectedTile"
      :viewportHeight="viewportHeight"
      :char="char"
    />
    <map-row
      :aspectRatio="aspectRatio"
      :tiles="configuration.row4"
      :selectTile="selectTile"
      :selectedTile="selectedTile"
      :viewportHeight="viewportHeight"
      :char="char"
    />
  </div>
</template>

<script>
import MapRow from './MapRow'
import tiles from '../lib/tiles'
import {getRandom} from '../lib/utils'

export default {
  name: 'game-map',
  components: {
    MapRow,
  },
  props: [
    'selectTile',
    'selectedTile',
    'aspectRatio',
    'viewportHeight',
    'backgroundColor',
    'char',
    'message',
  ],
  computed: {
    configuration() {
      return this.randomConfiguration()
    },
  },
  methods: {
    randomConfiguration() {
      const randomNum = getRandom(1, 4)
      const randomInt = Math.floor(Math.random() * 3)
      const buildings = tiles.filter(tile => tile.type !== 'road')
        .slice().sort(() => (randomInt >= 1 ? 1 : -1))
      const roads = tiles.filter(tile => tile.type === 'road')
        .slice().sort(() => (randomInt >= 1 ? 1 : -1))

      /* eslint-disable max-len */
      switch (randomNum) {

        case 1:
          return {
            row1: [buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop(), buildings.pop()],
            row2: [buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadSE'})],
            row3: [Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadTN'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadTS'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadNW'})],
            row4: [buildings.pop(), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop()],
          }

        case 2:
          return {
            row1: [buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNE'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadSW'})],
            row2: [buildings.pop(), buildings.pop(), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'})],
            row3: [Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadNW'})],
            row4: [buildings.pop(), buildings.pop(), buildings.pop(), buildings.pop()],
          }

        case 3:
          return {
            row1: [buildings.pop(), buildings.pop(), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'})],
            row2: [Object.defineProperty(roads.pop(), 'type', {value: 'roadSE'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadTN'})],
            row3: [Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop(), buildings.pop(), buildings.pop()],
            row4: [Object.defineProperty(roads.pop(), 'type', {value: 'roadNE'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadSW'}), buildings.pop(), buildings.pop()],
          }

        case 4:
          return {
            row1: [buildings.pop(), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop()],
            row2: [Object.defineProperty(roads.pop(), 'type', {value: 'roadSE'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadNEWS'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'})],
            row3: [Object.defineProperty(roads.pop(), 'type', {value: 'roadNW'}), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop()],
            row4: [buildings.pop(), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop()],
          }

        default:
          return {
            row1: [buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop(), buildings.pop()],
            row2: [buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadSE'})],
            row3: [Object.defineProperty(roads.pop(), 'type', {value: 'roadEW'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadTN'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadTS'}), Object.defineProperty(roads.pop(), 'type', {value: 'roadNW'})],
            row4: [buildings.pop(), buildings.pop(), Object.defineProperty(roads.pop(), 'type', {value: 'roadNS'}), buildings.pop()],
          }

      }
      /* eslint-enable max-len */
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  background-color: gray;
}

.show {
  display: flex;
  align-items: center;
  justify-content: center;
}

.hide {
  display: none;
}

.mapPortrait {
  width: calc(100vw);
  flex-wrap: wrap;
}

.mapLandscape {
  width: calc(50vw);
  flex-direction: column;
  flex-wrap: nowrap;
}
</style>
