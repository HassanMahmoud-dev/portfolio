<template>
  <Transition name="fade">
    <div v-if="isOpen" class="fixed inset-0 z-[100] flex items-center justify-center bg-background/90 backdrop-blur-2xl p-4 md:p-12" @click.self="close">
      <!-- Close Button -->
      <button @click="close" class="absolute top-8 right-8 z-[110] w-12 h-12 rounded-full bg-surface-container-high/50 hover:bg-primary text-on-surface hover:text-on-primary transition-all flex items-center justify-center border border-outline-variant/20 shadow-2xl">
        <span class="material-symbols-outlined">close</span>
      </button>

      <!-- Navigation Buttons -->
      <button v-if="images.length > 1" @click="prev" class="absolute left-4 md:left-8 top-1/2 -translate-y-1/2 z-[110] w-14 h-14 rounded-2xl bg-surface-container-high/50 hover:bg-primary text-on-surface hover:text-on-primary transition-all flex items-center justify-center border border-outline-variant/20 shadow-2xl backdrop-blur-md group">
        <span class="material-symbols-outlined transition-transform group-hover:-translate-x-1">arrow_back_ios_new</span>
      </button>
      
      <button v-if="images.length > 1" @click="next" class="absolute right-4 md:right-8 top-1/2 -translate-y-1/2 z-[110] w-14 h-14 rounded-2xl bg-surface-container-high/50 hover:bg-primary text-on-surface hover:text-on-primary transition-all flex items-center justify-center border border-outline-variant/20 shadow-2xl backdrop-blur-md group">
        <span class="material-symbols-outlined transition-transform group-hover:translate-x-1">arrow_forward_ios</span>
      </button>

      <!-- Main Image Container -->
      <div class="relative max-w-6xl w-full h-full flex flex-col items-center justify-center gap-8">
        <div class="relative group w-full h-[70vh] flex items-center justify-center">
          <Transition :name="slideDirection" mode="out-in">
            <img 
              :key="currentIndex" 
              :src="images[currentIndex]" 
              class="max-w-full max-h-full object-contain rounded-3xl shadow-[0_40px_80px_rgba(0,0,0,0.4)] border border-outline-variant/10"
              @click.stop
            />
          </Transition>
        </div>

        <!-- Thumbnails / Indicators -->
        <div class="flex gap-3 overflow-x-auto pb-4 max-w-full no-scrollbar">
          <button 
            v-for="(img, index) in images" 
            :key="index"
            @click="currentIndex = index"
            class="relative shrink-0 w-20 h-20 rounded-xl overflow-hidden border-2 transition-all duration-300"
            :class="currentIndex === index ? 'border-primary ring-4 ring-primary/20 scale-110' : 'border-transparent opacity-40 hover:opacity-100 scale-95'"
          >
            <img :src="img" class="w-full h-full object-cover" />
          </button>
        </div>

        <!-- Info -->
        <div class="text-center space-y-2">
          <p class="text-on-surface-variant font-medium tracking-widest uppercase text-xs">Image {{ currentIndex + 1 }} of {{ images.length }}</p>
          <p class="text-on-surface text-xl font-bold tracking-tight">{{ title }}</p>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps<{
  isOpen: boolean
  images: string[]
  startIndex: number
  title: string
}>()

const emit = defineEmits(['close'])

const currentIndex = ref(props.startIndex)
const slideDirection = ref('slide-right')

watch(() => props.startIndex, (newVal) => {
  currentIndex.value = newVal
})

watch(() => props.isOpen, (newVal) => {
  if (newVal) {
    currentIndex.value = props.startIndex
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
})

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
window.addEventListener('keydown', (e) => {
  if (!props.isOpen) return
  if (e.key === 'Escape') close()
  if (e.key === 'ArrowRight') next()
  if (e.key === 'ArrowLeft') prev()
})
</script>

<style scoped>
.fade-enter-active, .fade-leave-active { transition: opacity 0.4s ease, backdrop-filter 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; backdrop-filter: blur(0px); }

.slide-right-enter-active, .slide-right-leave-active,
.slide-left-enter-active, .slide-left-leave-active {
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.slide-right-enter-from { opacity: 0; transform: translateX(50px) scale(0.9); }
.slide-right-leave-to { opacity: 0; transform: translateX(-50px) scale(0.9); }

.slide-left-enter-from { opacity: 0; transform: translateX(-50px) scale(0.9); }
.slide-left-leave-to { opacity: 0; transform: translateX(50px) scale(0.9); }

.no-scrollbar::-webkit-scrollbar { display: none; }
.no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
</style>
