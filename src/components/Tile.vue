<template>
  <div class="tile" v-on:click="select()">
    <div :class="{desaturate: tile.walked, icon: true, grass: true}" style="background-image: url('static/icons/grass.png'); background-size: cover;" v-if="tile.type === 'grass'">
      <img v-if="hasPlayer" class="player" src="static/icons/player.png" />
    </div>
    <div :class="{desaturate: tile.walked, icon: true, tree: true}" style="background-image: url('static/icons/tree.png'); background-size: cover;" v-else>
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
  width: 30vh;
  height: 30vh;
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
