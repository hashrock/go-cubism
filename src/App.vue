<script setup lang="ts">
import { ref, onMounted, watch } from 'vue'
import Square from './components/Square.vue'

const gridSize = 20 // 20x20のグリッド
const squares = Array.from({ length: gridSize * gridSize }, (_, i) => ({
  x: (i % gridSize) * 100,
  y: Math.floor(i / gridSize) * 100
}))

// URLからの状態復元
const loadStateFromUrl = () => {
  const params = new URLSearchParams(window.location.search)
  const state = params.get('state')
  if (state) {
    try {
      const decoded = atob(state)
      const modes = decoded.split('').map(char => parseInt(char))
      squareModes.value = modes.length === gridSize * gridSize ? modes : Array(gridSize * gridSize).fill(1)
    } catch {
      squareModes.value = Array(gridSize * gridSize).fill(1)
    }
  } else {
    squareModes.value = Array(gridSize * gridSize).fill(1)
  }
}

// 状態をURLに保存
const saveStateToUrl = () => {
  const state = btoa(squareModes.value.join(''))
  const url = new URL(window.location.href)
  url.searchParams.set('state', state)
  window.history.replaceState({}, '', url)
}

const squareModes = ref<number[]>([])

onMounted(() => {
  loadStateFromUrl()
})

watch(squareModes, () => {
  saveStateToUrl()
}, { deep: true })

const handleClick = (index: number) => {
  const currentMode = squareModes.value[index]
  squareModes.value[index] = currentMode >= 5 ? 1 : currentMode + 1
}
</script>

<template>
  <div class="background">
    <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 2000 2000">
      <rect width="100%" height="100%" fill="white"/>
      <Square
        v-for="(pos, i) in squares"
        :key="i"
        :x="pos.x"
        :y="pos.y"
        :mode="squareModes[i]"
        @click="handleClick(i)"
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
