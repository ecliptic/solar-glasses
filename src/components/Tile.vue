<template>
  <div class="tile" v-on:click="select()">
    <div class="icon" v-if="tile.type === 'grass'">
      <img v-if="hasPlayer" class="player" src="static/icons/player.png" />
    </div>
    <div style="background-image: url('static/icons/tree.png'); background-size: cover;" class="icon tree" v-else>
      <img v-if="hasPlayer" class="player" src="static/icons/player.png" />
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
  display: flex;
  justify-content: center;
  align-items: center;
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
  background: brown;
}

.player {
  width: 100%;
  height: 100%;
}
</style>
