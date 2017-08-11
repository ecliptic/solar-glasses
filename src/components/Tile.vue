<template>
  <div class="tile">
    <div class="icon" v-if="type === 'grass'" />
    <div v-else src="../../assets/images/icons/tree.png">
      <img class="icon" src="../../assets/images/icons/tree.png" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tile',
  props: [
    'type',
  ],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tile {
  width: 30vh;
  height: 30vh;
  background-color: green;
}

.icon {
  width: 100%;
  height: 100%;
}
</style>
