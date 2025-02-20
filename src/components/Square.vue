<script setup lang="ts">
defineProps<{
  x: number
  y: number
}>()
</script>

<template>
  <g>
    <rect
      :x="x"
      :y="y"
      width="100"
      height="100"
      fill="none"
      stroke="black"
      stroke-width="1"
    />
    <line
      :x1="x"
      :y1="y"
      :x2="x + 100"
      :y2="y + 100"
      stroke="black"
      stroke-width="1"
    />
  </g>
</template> 