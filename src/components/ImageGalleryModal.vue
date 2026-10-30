<template>
  <Transition name="fade">
    <div
      v-if="isOpen"
      class="fixed inset-0 z-[100] flex items-center justify-center bg-background/95 backdrop-blur-xl p-4 md:p-10"
      @click.self="close"
    >
      <!-- Top Bar -->
      <div
        class="absolute top-0 left-0 right-0 h-16 flex items-center justify-between px-6 md:px-10 z-[110] border-b border-outline-variant/60 bg-background/80 backdrop-blur-md"
      >
        <div class="flex items-center gap-3">
          <span class="font-mono text-xs text-primary">GALLERY</span>
          <span class="text-outline-variant">/</span>
          <h3 class="text-on-surface font-medium text-sm truncate max-w-[200px] md:max-w-[400px]">
            {{ title }}
          </h3>
        </div>
        <div class="flex items-center gap-3">
          <span
            class="bg-surface-container-high px-2.5 py-1 rounded-md font-mono text-xs text-on-surface-variant border border-outline-variant"
          >
            {{ currentIndex + 1 }} / {{ images.length }}
          </span>
          <button
            @click="close"
            class="w-9 h-9 rounded-lg bg-surface-container-high hover:bg-primary text-on-surface hover:text-on-primary transition-colors duration-200 flex items-center justify-center border border-outline-variant cursor-pointer"
            aria-label="Close modal"
          >
            <span class="material-symbols-outlined text-[18px]">close</span>
          </button>
        </div>
      </div>

      <!-- Navigation Buttons -->
      <button
        v-if="images.length > 1"
        @click="prev"
        class="absolute left-3 md:left-8 top-1/2 -translate-y-1/2 z-[110] w-11 h-11 rounded-xl bg-surface-container-high/90 hover:bg-primary text-on-surface hover:text-on-primary transition-colors duration-200 flex items-center justify-center border border-outline-variant shadow-lg cursor-pointer"
        aria-label="Previous image"
      >
        <span class="material-symbols-outlined text-[18px]">arrow_back</span>
      </button>

      <button
        v-if="images.length > 1"
        @click="next"
        class="absolute right-3 md:right-8 top-1/2 -translate-y-1/2 z-[110] w-11 h-11 rounded-xl bg-surface-container-high/90 hover:bg-primary text-on-surface hover:text-on-primary transition-colors duration-200 flex items-center justify-center border border-outline-variant shadow-lg cursor-pointer"
        aria-label="Next image"
      >
        <span class="material-symbols-outlined text-[18px]">arrow_forward</span>
      </button>

      <!-- Main Image Container -->
      <div
        class="relative max-w-5xl w-full h-full flex flex-col items-center justify-center gap-5 mt-12"
      >
        <div class="relative w-full flex-1 min-h-0 flex items-center justify-center">
          <Transition :name="slideDirection" mode="out-in">
            <img
              :key="currentIndex"
              :src="images[currentIndex]"
              :alt="`${title} screenshot ${currentIndex + 1}`"
              class="max-w-full max-h-[64vh] md:max-h-[68vh] object-contain rounded-xl shadow-2xl border border-outline-variant"
              @click.stop
            />
          </Transition>
        </div>

        <!-- Thumbnails -->
        <div class="flex gap-2.5 overflow-x-auto pb-2 max-w-full no-scrollbar px-4">
          <button
            v-for="(img, index) in images"
            :key="index"
            @click="currentIndex = index"
            class="relative shrink-0 w-16 h-12 md:w-20 md:h-14 rounded-lg overflow-hidden border transition-all duration-200 cursor-pointer"
            :class="
              currentIndex === index
                ? 'border-primary ring-2 ring-primary/30 opacity-100'
                : 'border-outline-variant opacity-45 hover:opacity-80'
            "
          >
            <img :src="img" class="w-full h-full object-cover" />
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
import { ref, watch, onMounted, onUnmounted } from 'vue'

const props = defineProps<{
  isOpen: boolean
  images: string[]
  startIndex: number
  title: string
}>()

const emit = defineEmits(['close'])

const currentIndex = ref(props.startIndex)
const slideDirection = ref('slide-right')

watch(
  () => props.startIndex,
  (newVal) => {
    currentIndex.value = newVal
  },
)

watch(
  () => props.isOpen,
  (newVal) => {
    if (newVal) {
      currentIndex.value = props.startIndex
      document.body.style.overflow = 'hidden'
    } else {
      document.body.style.overflow = ''
    }
  },
)

function close() {
  emit('close')
}

function next() {
  slideDirection.value = 'slide-right'
  currentIndex.value = (currentIndex.value + 1) % props.images.length
}

function prev() {
  slideDirection.value = 'slide-left'
  currentIndex.value = (currentIndex.value - 1 + props.images.length) % props.images.length
}

function handleKeydown(e: KeyboardEvent) {
  if (!props.isOpen) return
  if (e.key === 'Escape') close()
  if (e.key === 'ArrowRight') next()
  if (e.key === 'ArrowLeft') prev()
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(24px);
}
.slide-right-leave-to {
  opacity: 0;
  transform: translateX(-24px);
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(-24px);
}
.slide-left-leave-to {
  opacity: 0;
  transform: translateX(24px);
}
</style>
