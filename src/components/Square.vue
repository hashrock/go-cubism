<script setup lang="ts">
const props = defineProps<{
  x: number
  y: number
  mode?: number
}>()

const emit = defineEmits<{
  (e: 'click', event: MouseEvent): void
}>()
</script>

<template>
  <g @click="$emit('click', $event)">
    <rect
      :x="x"
      :y="y"
      width="100"
      height="100"
      :fill="mode === 5 ? 'black' : 'white'"
      stroke="black"
      stroke-width="1"
      :class="{ 'animate-dash': mode === 1 }"
    />
    <line
      v-if="mode === 2"
      :x1="x"
      :y1="y"
      :x2="x + 100"
      :y2="y + 100"
      stroke="black"
      stroke-width="1"
      class="animate-dash diagonal"
    />
    <path
      v-if="mode === 3"
      :d="`M ${x + 100} ${y} L ${x + 100} ${y + 100} L ${x} ${y} Z`"
      fill="black"
    />
    <path
      v-if="mode === 4"
      :d="`M ${x} ${y + 100} L ${x + 100} ${y + 100} L ${x} ${y} Z`"
      fill="none"
      stroke="black"
      stroke-width="2"
      class="animate-dash triangle"
    />
  </g>
</template>

<style scoped>
.animate-dash {
  stroke-dasharray: 300;
  animation: dash 0.5s linear forwards;
}

.diagonal {
  stroke-dasharray: 300;
}

.triangle {
  stroke-dasharray: 300;
}

@keyframes dash {
  from {
    stroke-dashoffset: 300;
  }
  to {
    stroke-dashoffset: 0;
  }
}
</style> 