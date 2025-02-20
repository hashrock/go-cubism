<script setup lang="ts">
defineProps<{
    x: number
    y: number
    size: number
    mode?: number
}>()

defineEmits<{
    (e: 'click', event: MouseEvent): void
}>()
</script>

<template>
    <g @click="$emit('click', $event)" class="square-group">
        <rect :x="x" :y="y" :width="size" :height="size" :fill="mode === 5 ? 'black' : 'white'" stroke="black"
            stroke-width="1" :class="{ 'animate-dash': mode === 1 }" />
        <line v-if="mode === 2" :x1="x" :y1="y" :x2="x + size" :y2="y + size" stroke="black" stroke-width="1"
            class="animate-dash diagonal" />
        <path v-if="mode === 3" :d="`M ${x + size} ${y} L ${x + size} ${y + size} L ${x} ${y} Z`" fill="black" />
        <path v-if="mode === 4" :d="`M ${x} ${y + size} L ${x + size} ${y + size} L ${x} ${y} Z`" fill="none"
            stroke="black" stroke-width="2" class="animate-dash triangle" />
        <rect :x="x" :y="y" :width="size" :height="size" class="hover-overlay" fill="gray" fill-opacity="0"
            stroke="none" />
    </g>
</template>

<style scoped>
.animate-dash {
    stroke-dasharray: 450;
    animation: dash 0.5s linear forwards;
}

.diagonal {
    stroke-dasharray: 450;
}

.triangle {
    stroke-dasharray: 450;
}

@keyframes dash {
    from {
        stroke-dashoffset: 450;
    }

    to {
        stroke-dashoffset: 0;
    }
}

.square-group {
    cursor: pointer;
}

.hover-overlay {
    transition: fill-opacity 0.2s ease;
}

.square-group:hover .hover-overlay {
    fill-opacity: 0.1;
}
</style>