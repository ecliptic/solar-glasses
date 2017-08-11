<template>
  <div class="card">
    <img class="image" src="image" />
    <div  />
    <Tile v-for="tile in row3" />
  </div>
</template>

<script>
import Tile from './Tile'
export default {
  name: 'Map',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  position: absolute;
  width: 66%;
  height: 90%;
  background-color: white;
}

.image {

}
</style>
