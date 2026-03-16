<template>
  <div
    class="placeholder-image"
    :style="{ aspectRatio: ratio, width: width ?? '100%' }"
    :aria-label="label"
    role="img"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="100%"
      height="100%"
      viewBox="0 0 400 300"
      preserveAspectRatio="xMidYMid slice"
    >
      <!-- Background -->
      <rect width="400" height="300" :fill="bgColor" rx="0" />

      <!-- Subtle grid -->
      <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
        <path d="M 40 0 L 0 0 0 40" fill="none" :stroke="lineColor" stroke-width="0.5" />
      </pattern>
      <rect width="400" height="300" fill="url(#grid)" />

      <!-- Center icon -->
      <g transform="translate(200, 135)">
        <rect x="-28" y="-22" width="56" height="44" rx="4" :fill="iconColor" />
        <circle cx="0" cy="-5" r="9" :fill="bgColor" opacity="0.6" />
        <path d="M -28 10 L -12 -4 L 0 8 L 14 -2 L 28 10 L 28 22 L -28 22 Z" :fill="bgColor" opacity="0.6" />
      </g>

      <!-- Label -->
      <text
        v-if="label"
        x="200"
        y="200"
        text-anchor="middle"
        dominant-baseline="middle"
        font-family="system-ui, -apple-system, sans-serif"
        font-size="13"
        font-weight="500"
        letter-spacing="0.03em"
        :fill="textColor"
      >
        {{ label }}
      </text>

      <!-- Dimension hint -->
      <text
        v-if="showSize"
        x="200"
        y="220"
        text-anchor="middle"
        dominant-baseline="middle"
        font-family="system-ui, -apple-system, sans-serif"
        font-size="11"
        :fill="textColor"
        opacity="0.5"
      >
        {{ hint }}
      </text>
    </svg>
  </div>
</template>

<script setup lang="ts">
const props = withDefaults(defineProps<{
  /** Descriptive label shown inside the placeholder */
  label?: string
  /** Aspect ratio string e.g. '16/9', '1/1', '4/3' */
  ratio?: string
  /** Explicit width override e.g. '320px', '100%' */
  width?: string
  /** Size hint shown below the label e.g. '1200 × 630' */
  hint?: string
  /** Show the size hint */
  showSize?: boolean
  /** Color theme: 'neutral' | 'warm' | 'cool' */
  theme?: 'neutral' | 'warm' | 'cool'
}>(), {
  label: 'Image placeholder',
  ratio: '16/9',
  showSize: false,
  theme: 'neutral',
})

const bgColor = computed(() => ({
  neutral: '#F2F2F0',
  warm:    '#F5F0EB',
  cool:    '#EEF1F6',
}[props.theme]))

const lineColor = computed(() => ({
  neutral: '#D8D8D4',
  warm:    '#DDD5CA',
  cool:    '#CDD5E0',
}[props.theme]))

const iconColor = computed(() => ({
  neutral: '#C8C8C4',
  warm:    '#CCBFB2',
  cool:    '#BFCAD6',
}[props.theme]))

const textColor = computed(() => ({
  neutral: '#8C8C8A',
  warm:    '#8C7E72',
  cool:    '#6E7E8C',
}[props.theme]))
</script>

<style scoped>
.placeholder-image {
  display: block;
  overflow: hidden;
  border-radius: inherit;
}
</style>
