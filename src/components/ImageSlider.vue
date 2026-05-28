<script setup lang="ts">
import gsap from 'gsap'
import { computed, onMounted, onUnmounted, ref } from 'vue'

const props = withDefaults(defineProps<{
  images: string[]
  autoPlay?: boolean
  interval?: number
  showArrows?: boolean
  showDots?: boolean
  aspectRatio?: string
}>(), {
  autoPlay: true,
  interval: 4000,
  showArrows: true,
  showDots: true,
  aspectRatio: '16/9',
})

const currentIndex = ref(0)
const isAnimating = ref(false)
const containerRef = ref<HTMLElement | null>(null)
const trackRef = ref<HTMLElement | null>(null)
const isHovered = ref(false)
const touchStartX = ref(0)
const touchEndX = ref(0)
const isDragging = ref(false)

let autoPlayTimer: ReturnType<typeof setInterval> | null = null

const total = computed(() => props.images.length)

function goTo(index: number) {
  if (isAnimating.value || index === currentIndex.value || !containerRef.value || !trackRef.value) return
  isAnimating.value = true

  gsap.to(trackRef.value, {
    x: -index * containerRef.value.offsetWidth,
    duration: 0.5,
    ease: 'power2.inOut',
    onComplete: () => { isAnimating.value = false },
  })

  currentIndex.value = index
  resetAutoPlay()
}

function next() {
  if (isAnimating.value) return
  goTo((currentIndex.value + 1) % total.value)
}

function prev() {
  if (isAnimating.value) return
  goTo((currentIndex.value - 1 + total.value) % total.value)
}

function startAutoPlay() {
  if (!props.autoPlay || total.value <= 1) return
  stopAutoPlay()
  autoPlayTimer = setInterval(() => {
    if (!isHovered.value) next()
  }, props.interval)
}

function stopAutoPlay() {
  if (autoPlayTimer) {
    clearInterval(autoPlayTimer)
    autoPlayTimer = null
  }
}

function resetAutoPlay() {
  stopAutoPlay()
  startAutoPlay()
}

function onTouchStart(e: TouchEvent) {
  const touch = e.touches[0]
  if (!touch) return
  isDragging.value = true
  touchStartX.value = touch.clientX
}

function onTouchMove(e: TouchEvent) {
  if (!isDragging.value) return
  const touch = e.touches[0]
  if (!touch) return
  touchEndX.value = touch.clientX
}

function onTouchEnd() {
  if (!isDragging.value) return
  isDragging.value = false
  const diff = touchStartX.value - touchEndX.value
  if (Math.abs(diff) > 50) {
    if (diff > 0) next()
    else prev()
  }
}

onMounted(() => { startAutoPlay() })
onUnmounted(() => { stopAutoPlay() })
</script>

<template>
  <div
    ref="containerRef"
    class="relative overflow-hidden w-[536px] select-none absolute mt-[-500px] ml-[650px]"
    :style="{ aspectRatio: props.aspectRatio }"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
    @touchstart="onTouchStart"
    @touchmove="onTouchMove"
    @touchend="onTouchEnd"
  >
    <div ref="trackRef" class="flex will-change-transform">
      <img
        v-for="(src, i) in images"
        :key="i"
        :src="src"
        :alt="`slide-${i + 1}`"
        class="w-full flex-shrink-0 object-cover"
        draggable="false"
      />
    </div>

    <button
      v-if="showArrows && total > 1"
      class="absolute left-3 top-1/2 -translate-y-1/2 w-10 h-10 flex items-center justify-center rounded-full bg-black/30 text-white hover:bg-black/50 transition-colors cursor-pointer z-10"
      @click="prev"
    >
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
      </svg>
    </button>

    <button
      v-if="showArrows && total > 1"
      class="absolute right-3 top-1/2 -translate-y-1/2 w-10 h-10 flex items-center justify-center rounded-full bg-black/30 text-white hover:bg-black/50 transition-colors cursor-pointer z-10"
      @click="next"
    >
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
      </svg>
    </button>

    <div
      v-if="showDots && total > 1"
      class="absolute bottom-4 left-1/2 -translate-x-1/2 flex gap-2 z-10"
    >
      <button
        v-for="(_, i) in images"
        :key="i"
        class="w-2.5 h-2.5 rounded-full transition-all cursor-pointer"
        :class="i === currentIndex ? 'bg-white scale-125' : 'bg-white/50 hover:bg-white/70'"
        @click="goTo(i)"
      />
    </div>
  </div>
</template>
