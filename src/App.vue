<script setup lang="ts">
const gridSize = 20 // 20x20のグリッド
const squares = Array.from({ length: gridSize * gridSize }, (_, i) => ({
  x: (i % gridSize) * 100,
  y: Math.floor(i / gridSize) * 100
}))
</script>

<template>
  <div class="background">
    <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 2000 2000">
      <rect width="100%" height="100%" fill="white"/>
      <rect
        v-for="(pos, i) in squares"
        :key="i"
        :x="pos.x"
        :y="pos.y"
        width="100"
        height="100"
        fill="none"
        stroke="black"
        stroke-width="1"
      />
    </svg>
  </div>
</template>

<style scoped>
.background {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.background svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
