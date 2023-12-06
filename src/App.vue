<template>
  <div class="flex flex-col justify-center items-center py-28">
    <GameBoard />
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue'

export default{
  components: {
    GameBoard
  }
}
</script>

<style>
body {
  color: #fff;
  background: #000;
  min-height: 100vh;
}
</style>
