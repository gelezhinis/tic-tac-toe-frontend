<template>
  <h3 v-if="winner">The Winner is {{winner}}</h3>
  <h3 v-else-if="isDraw">Draw Game</h3>
  <h3 v-else>Next Move {{player}}</h3>
</template>

<script>
export default {
  props: ['player', 'winner', 'isDraw']
}
</script>

<style>

</style>