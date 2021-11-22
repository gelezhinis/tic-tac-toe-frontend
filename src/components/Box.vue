<template>
  <div class="board-box" @click="onClick">
    <span>{{value}}</span>
  </div>
</template>

<script>
export default {
  props: ['value'],
  inheritAttrs: false,
  methods: {
    onClick() {
      this.$emit('click');
    }
  }
}
</script>

<style>
  .board-box {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #666;
    border: 5px solid #333;
    border-radius: 10px;
    font-weight: bold;
    font-size: 4em;
    transition: all 0.1s;
    cursor: pointer;
  }
</style>