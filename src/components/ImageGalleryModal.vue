<template>
  <Transition name="fade">
    <div
      v-if="isOpen"
      class="fixed inset-0 z-[100] flex items-center justify-center bg-background/95 backdrop-blur-3xl p-4 md:p-12"
      @click.self="close"
    >
      <!-- Title Bar -->
      <div
        class="absolute top-0 left-0 right-0 h-16 md:h-20 flex items-center justify-between px-6 md:px-10 z-[110] bg-gradient-to-b from-background/80 to-transparent"
      >
        <div class="flex items-center gap-3">
          <span class="material-symbols-outlined text-primary text-xl">photo_library</span>
          <h3
            class="text-on-surface font-bold text-sm md:text-base font-headline truncate max-w-[200px] md:max-w-[400px]"
          >
            {{ title }}
          </h3>
        </div>
        <div class="flex items-center gap-3">
          <!-- Image Counter Pill -->
          <span
            class="bg-surface-container-high/80 backdrop-blur-sm px-3 py-1 rounded-full text-xs font-bold text-on-surface-variant border border-outline-variant/15"
          >
            {{ currentIndex + 1 }} / {{ images.length }}
          </span>
          <button
            @click="close"
            class="w-10 h-10 rounded-xl bg-surface-container-high/50 hover:bg-primary text-on-surface hover:text-on-primary transition-all duration-300 flex items-center justify-center border border-outline-variant/15 shadow-lg"
          >
            <span class="material-symbols-outlined text-lg">close</span>
          </button>
        </div>
      </div>

      <!-- Navigation Buttons -->
      <button
        v-if="images.length > 1"
        @click="prev"
        class="absolute left-3 md:left-8 top-1/2 -translate-y-1/2 z-[110] w-12 h-12 md:w-14 md:h-14 rounded-2xl bg-surface-container-high/50 hover:bg-primary text-on-surface hover:text-on-primary transition-all duration-300 flex items-center justify-center border border-outline-variant/15 shadow-xl backdrop-blur-md group"
      >
        <span class="material-symbols-outlined transition-transform group-hover:-translate-x-0.5"
          >arrow_back_ios_new</span
        >
      </button>

      <button
        v-if="images.length > 1"
        @click="next"
        class="absolute right-3 md:right-8 top-1/2 -translate-y-1/2 z-[110] w-12 h-12 md:w-14 md:h-14 rounded-2xl bg-surface-container-high/50 hover:bg-primary text-on-surface hover:text-on-primary transition-all duration-300 flex items-center justify-center border border-outline-variant/15 shadow-xl backdrop-blur-md group"
      >
        <span class="material-symbols-outlined transition-transform group-hover:translate-x-0.5"
          >arrow_forward_ios</span
        >
      </button>

      <!-- Main Image Container -->
      <div
        class="relative max-w-6xl w-full h-full flex flex-col items-center justify-center gap-6 mt-12"
      >
        <div class="relative group w-full flex-1 min-h-0 flex items-center justify-center">
          <Transition :name="slideDirection" mode="out-in">
            <img
              :key="currentIndex"
              :src="images[currentIndex]"
              class="max-w-full max-h-[60vh] md:max-h-[65vh] object-contain rounded-2xl md:rounded-3xl shadow-[0_40px_80px_rgba(0,0,0,0.4)] border border-outline-variant/10"
              @click.stop
            />
          </Transition>
        </div>

        <!-- Thumbnails -->
        <div class="flex gap-2 md:gap-3 overflow-x-auto pb-4 max-w-full no-scrollbar px-4">
          <button
            v-for="(img, index) in images"
            :key="index"
            @click="currentIndex = index"
            class="relative shrink-0 w-16 h-16 md:w-20 md:h-20 rounded-xl overflow-hidden border-2 transition-all duration-300"
            :class="
              currentIndex === index
                ? 'border-primary ring-4 ring-primary/20 scale-110 shadow-[0_0_20px_var(--primary-glow)]'
                : 'border-transparent opacity-40 hover:opacity-80 scale-95'
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

// Keyboard support
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
  transition: opacity 0.4s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(60px) scale(0.92);
}
.slide-right-leave-to {
  opacity: 0;
  transform: translateX(-60px) scale(0.92);
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(-60px) scale(0.92);
}
.slide-left-leave-to {
  opacity: 0;
  transform: translateX(60px) scale(0.92);
}
</style>
