<template>
  <h1>-=XOX=-</h1>
  <GameBoard />
</template>

<script>
import GameBoard from './components/GameBoard.vue';
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  components: {GameBoard}
}
</script>

<style>
  #app {
    font-family: Arial, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: black;
    margin-top: 60px;
  }
</style>
