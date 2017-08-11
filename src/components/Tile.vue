<template>
  <div class="tile" v-on:click="select()">
    <div class="icon" v-if="tile.type === 'grass'"></div>
    <div v-else>
      <img class="tree" src="static/icons/tree.png" />
    </div>
    <div v-if="hasPlayer">
      <img class="player" src="static/icons/player.png" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tile',
  props: [
    'tile',
    'hasPlayer',
    'selectTile'
  ],
  methods: {
    select () {
      this.selectTile(this.tile)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tile {
  width: 30vh;
  height: 30vh;
  background: green;
  outline-width: 2px;
  outline-color: black;
  display: inline-block;
  cursor: pointer;
}

.icon {
  width: 100%;
  height: 100%;
}

.tree {
  width: 100%;
  height: 100%;
  background: brown;
}

.player {
  width: 100%;
  height: 100%;
}
</style>
