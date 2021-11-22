<template>
  <div class="backdrop">
    <div class="modal">
      <PlayStatus :winner="winner" :isDraw="isDraw" />
      <Button title="Play Again" />    
    </div>
  </div>
</template>

<script>
import Button from './Button.vue'
import PlayStatus from './PlayStatus.vue';

export default {
  components: {Button, PlayStatus},
  props: ['winner', 'isDraw']
};
</script>

<style>
.modal {
  font-family: Arial;
  font-size: 24px;
  width: 400px;
  padding: 20px;
  margin: 270px auto;
  background: #aaa;
  border-radius: 10px;
}
.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
</style>
