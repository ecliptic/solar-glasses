<template>
  <div class="card">
    <div class="image" />
    <div class="message" />
    <div class="actions">
      <button class="action">
        live
      </button>
      <button class="action">
        die
      </button>
    </div>
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
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  left: 50%;
  top: 50%;
  transform: translate(-50% -50%);
  width: 66%;
  height: 90%;
  background-color: white;
}

.image {
  width: 75%;
  height: 40%;
}

.message {
  width: 75%;
  height: 30%;
}

.actions {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 75%;
  height: 30%;
}

.action {
  font-size: 16px;
}
</style>
