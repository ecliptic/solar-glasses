<template>
  <div class="tile">
    <div class="icon" v-if="tile === 'grass'" />
    <div v-else src="../../assets/images/icons/tree.png">
      <img class="icon" src="../../assets/images/icons/tree.png" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tile',
  props: [
    'tile',
  ],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tile {
  width: 30vh;
  height: 30vh;
  background-color: green;
  outline-width: 2px;
  outline-color: black;
}

.icon {
  width: 100%;
  height: 100%;
}
</style>
