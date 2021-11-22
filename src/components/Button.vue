<template>
  <div>
    <button class="restart" @onClick="click">{{title}}</button>
  </div>
</template>

<script>
export default {
  props: ['title'],
  methods: {
    onClick() {
      this.$emit('click')
    }
  }
}
</script>

<style>
  .restart {
    width: 150px;
    height: 50px;
    border: 4px solid #333;
    border-radius: 8px;
    background-color: #333;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    margin: 20px auto;
    cursor: pointer
  }
  .restart:hover {
    background-color: #fff;
    color: #333;
    font-size: 18px;
    transition: background-color 0.7s ease-in;
  }
</style>