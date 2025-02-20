<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import Square from './components/Square.vue'
</script>

<template>
  <div class="background">
    <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
      <rect width="100%" height="100%" fill="white"/>
    </svg>
    <div class="content">
      <Square />
    </div>
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
  z-index: -1;
}

.content {
  position: relative;
  z-index: 1;
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
