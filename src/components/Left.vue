<template>
  <div class="left">
    left111
    <button @click="flytoHome">flyto</button>
    <button @click="flyto">2333</button>
  </div>
</template>
<script setup>
const flytoHome = () => {};
const flyto = () => {};
</script>
<style scoped>
.left {
  width: 200px;
  height: 100%;
  background-color: transparent;
  position: absolute;
  left: 0;
  top: 0;
  overflow: auto;
  padding: 10px;
  box-sizing: border-box;
  border-right: 1px solid #e0e0e0;
}
</style>
