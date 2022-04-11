<script setup>
import { computed } from 'vue'

const props = defineProps({
    size: {
      type: [Number, String],
      default: 36
    },
    maxValue: {
      type: [Number, String],
      default: 100,
    },
    minValue: {
      type: [Number, String],
      default: 0,
    },
    value: {
      type: [Number, String],
      default: 0,
    },
    strokeWidth: {
      type: [Number, String],
      default: 4
    },
    ringColor: {
      type: String,
      default: "#E9EBEE"
    },
    progressColor: {
      type: String,
      default: "#08D7B8"
    },
    showNumber: {
      type: Boolean,
      default: true
    },
    rotate: {
        type: String,
        default: '-90' 
    },
    fill: {
        type: String,
        default: '#cf1515'
    }
})

const r = computed(() => Number(props.size) / 2 - Number(props.strokeWidth) / 2);

const dasharray = computed(() => Number(props.maxValue) - Number(props.minValue));

const dashoffset = computed(() => dasharray.value - (Number(props.value) - Number(props.minValue)))

const progressNumber = computed(() => props.showNumber && parseInt(props.value));

</script>

<template>
  <div class="relative" :style="{width: `${size}px`,height: `${size}px`}" :data-pct="progressNumber">
    <svg :width="size" :height="size" :viewPort="`0 0 ${size} ${size}`" :style="{ transform: `rotate(${rotate}deg)`}">
      <circle
        :stroke="ringColor"
        :r="r"
        :cx="size/2"
        :cy="size/2"
        :stroke-width="strokeWidth"
        :fill="fill" />
      <circle
        class="percent"
        :stroke="progressColor"
        :r="r"
        :cx="size/2"
        :cy="size/2"
        :stroke-width="strokeWidth"
        fill="none"
        :pathLength="dasharray - 1"
        :stroke-dasharray="dasharray"
        :stroke-dashoffset="dashoffset"
      />
    </svg>
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 text-white">{{ value }}</div>
  </div>
</template>
