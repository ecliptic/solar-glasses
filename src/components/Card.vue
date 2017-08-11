<template>
  <div class="card">
    <div  />
    <Tile v-for="tile in row3" />
  </div>
</template>

<script>
export default {
  name: 'Card'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50% -50%);
  width: 66%;
  height: 90%;
  background-color: white;
}

.image {

}
</style>
