<template>
  <div class="container">
    <h1>Congratulation! You're realy lucky :)</h1>
    <button @click="newGame">New Game</button>
  </div>
</template>
<script>
export default {
  methods: {
    newGame() {
      this.$emit("activeComponentEvent", "app-game-card");
    }
  }
};
</script>

<style scoped>
.container {
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.container h1 {
  text-align: center;
  font-size: 333%;
  color: darkgreen;
  opacity: 0.5;
}

.container button {
  cursor: pointer;
  width: 200px;
  height: 50px;
  background-color: #fff;
  color: darkred;
  border: 1px solid darkgreen;
  font-size: 15px;
  border-radius: 5px;
  outline: none;
  transition: all 0.5s;
}

.container button:hover {
  background-color: darkgreen;
  color: #fff;
  transition: all 0.5s;
}
</style>

