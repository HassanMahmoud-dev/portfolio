<template>
  <!-- TopNavBar -->
  <header
    class="fixed top-0 w-full z-50 bg-background/70 backdrop-blur-xl shadow-[0_20px_40px_rgba(0,0,0,0.1)] transition-colors duration-300"
  >
    <nav class="flex justify-between items-center max-w-7xl mx-auto px-8 h-20">
      <div class="text-xl font-bold tracking-tighter text-on-surface">
        {{ currentData.personalInfo.name }}
      </div>
      <div class="hidden md:flex items-center gap-8">
        <button
          @click="scrollTo('about')"
          class="text-on-surface/60 hover:text-secondary transition-colors duration-300"
        >
          About
        </button>
        <button
          @click="scrollTo('skills')"
          class="text-on-surface/60 hover:text-secondary transition-colors duration-300"
        >
          Skills
        </button>
        <button
          @click="scrollTo('libraries')"
          class="text-on-surface/60 hover:text-secondary transition-colors duration-300"
        >
          Libraries
        </button>
        <button
          @click="scrollTo('projects')"
          class="text-on-surface/60 hover:text-secondary transition-colors duration-300"
        >
          Projects
        </button>
        <button
          @click="scrollTo('experience')"
          class="text-on-surface/60 hover:text-secondary transition-colors duration-300"
        >
          Experience
        </button>
      </div>
      <div class="flex items-center gap-4">
        <button
          @click="toggleTheme"
          class="w-10 h-10 rounded-xl flex items-center justify-center text-on-surface/60 hover:bg-surface-container transition-all"
          aria-label="Toggle Theme"
        >
          <span class="material-symbols-outlined">{{ isDark ? 'light_mode' : 'dark_mode' }}</span>
        </button>
        <div class="hidden md:flex items-center gap-3 text-on-surface/60">
          <span class="material-symbols-outlined">mail</span>
          <span class="material-symbols-outlined">account_circle</span>
        </div>
        <a
          class="bg-gradient-to-r from-primary to-primary-container text-on-primary px-6 py-2 rounded-lg font-bold hover:scale-95 transition-transform duration-200"
          :href="'mailto:' + currentData.personalInfo.email"
          >Contact</a
        >
      </div>
    </nav>
  </header>

  <main class="relative overflow-hidden pt-20">
    <!-- Tab Switcher -->
    <div class="max-w-7xl mx-auto px-8 mt-12 mb-8">
      <div class="flex justify-center">
        <div
          class="inline-flex p-1.5 bg-surface-container-high rounded-2xl border border-outline-variant/20 shadow-xl relative backdrop-blur-xl"
        >
          <button
            @click="activeTab = 'FullStack'"
            :class="[
              'relative z-10 px-8 py-3 rounded-xl text-sm font-bold transition-all duration-500',
              activeTab === 'FullStack'
                ? 'text-on-primary'
                : 'text-on-surface/60 hover:text-on-surface',
            ]"
          >
            Full Stack Developer
            <div
              v-if="activeTab === 'FullStack'"
              class="absolute inset-0 bg-gradient-to-r from-primary to-primary-container rounded-xl -z-10 transition-all duration-500"
            ></div>
          </button>
          <button
            @click="activeTab = 'Frontend'"
            :class="[
              'relative z-10 px-8 py-3 rounded-xl text-sm font-bold transition-all duration-500',
              activeTab === 'Frontend'
                ? 'text-on-primary'
                : 'text-on-surface/60 hover:text-on-surface',
            ]"
          >
            Frontend Developer
            <div
              v-if="activeTab === 'Frontend'"
              class="absolute inset-0 bg-gradient-to-r from-secondary to-secondary-container rounded-xl -z-10 transition-all duration-500"
            ></div>
          </button>
        </div>
      </div>
    </div>

    <!-- Hero Section -->
    <section
      id="hero"
      class="relative min-h-[921px] flex items-center justify-center px-8 py-24 overflow-hidden"
    >
      <div class="absolute inset-0 hero-gradient opacity-40"></div>
      <div class="max-w-7xl mx-auto grid md:grid-cols-2 gap-16 items-center relative z-10">
        <div class="space-y-8">
          <div class="space-y-4">
            <div
              class="flex items-center gap-2 text-secondary font-medium tracking-widest uppercase text-xs"
            >
              <span class="material-symbols-outlined text-sm">location_on</span>
              {{ currentData.personalInfo.location }}
            </div>
            <h1
              class="text-6xl md:text-[3.5rem] font-black leading-[1.1] tracking-tighter text-on-surface text-glow"
            >
              {{ currentData.personalInfo.name }}
            </h1>
            <p class="text-xl text-on-surface-variant font-light max-w-lg leading-relaxed">
              {{ currentProfile.role }} <span class="text-primary mx-2">·</span>
              {{ currentProfile.specialization }}
            </p>
          </div>
          <div class="flex flex-wrap gap-3">
            <span
              v-for="badge in currentProfile.heroBadges"
              :key="badge.name"
              :class="badge.color"
              class="px-4 py-1.5 rounded-full text-xs font-bold border"
            >
              {{ badge.name }}
            </span>
          </div>
          <div class="flex flex-col gap-4 text-on-surface-variant">
            <a
              class="flex items-center gap-3 hover:text-primary transition-colors group"
              :href="'mailto:' + currentData.personalInfo.email"
            >
              <span
                class="material-symbols-outlined text-primary group-hover:scale-110 transition-transform"
                >mail</span
              >
              {{ currentData.personalInfo.email }}
            </a>
            <a
              class="flex items-center gap-3 hover:text-primary transition-colors group"
              :href="'tel:' + currentData.personalInfo.phone"
            >
              <span
                class="material-symbols-outlined text-primary group-hover:scale-110 transition-transform"
                >call</span
              >
              {{ currentData.personalInfo.phone }}
            </a>
          </div>
          <div class="flex gap-6">
            <a
              class="text-on-surface-variant hover:text-secondary transition-all hover:scale-110"
              :href="currentData.personalInfo.linkedin"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="LinkedIn"
            >
              <i class="fa-brands fa-linkedin text-2xl"></i>
            </a>
            <a
              class="text-on-surface-variant hover:text-secondary transition-all hover:scale-110"
              :href="currentData.personalInfo.github"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="GitHub"
            >
              <i class="fa-brands fa-github text-2xl"></i>
            </a>
            <a
              class="text-on-surface-variant hover:text-secondary transition-all hover:scale-110"
              href="https://drive.google.com/file/d/1jLgM2r7PBa2IKNg_Ok81payeakBsQdUr/view"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="CV/Resume"
            >
              <i class="fa-solid fa-file-lines text-2xl"></i>
            </a>
          </div>
        </div>
        <div class="relative flex justify-center">
          <div class="relative w-fit h-fit">
            <div class="absolute inset-0 bg-primary/20 blur-3xl rounded-full scale-110"></div>
            <div
              class="relative rounded-[3rem] overflow-hidden border-2 border-on-surface/10 glass-card"
            >
              <img
                alt="Developer Portrait"
                class="w-full max-w-[20rem] md:max-w-[24rem] h-auto object-contain hover:scale-105 transition-all duration-700"
                src="/images/Mypicture.jpg"
              />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Content Sections -->
    <transition name="fade" mode="out-in">
      <component :is="activeTab === 'FullStack' ? FullStackSection : FrontendSection" />
    </transition>
  </main>

  <footer
    class="w-full border-t border-outline-variant/10 bg-background transition-colors duration-300"
  >
    <div
      class="flex flex-col md:flex-row justify-between items-center py-12 px-8 max-w-7xl mx-auto gap-4"
    >
      <div class="text-lg font-black text-on-surface">{{ currentData.personalInfo.name }}</div>
      <p class="text-[0.75rem] font-medium text-on-surface/40 tracking-wider">
        © 2024 {{ currentData.personalInfo.name }} • Digital Curator
      </p>
      <div class="flex gap-6">
        <a
          class="text-on-surface/40 hover:text-secondary transition-all hover:scale-125"
          :href="currentData.personalInfo.linkedin"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="LinkedIn"
        >
          <i class="fa-brands fa-linkedin text-lg"></i>
        </a>
        <a
          class="text-on-surface/40 hover:text-secondary transition-all hover:scale-125"
          :href="currentData.personalInfo.github"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="GitHub"
        >
          <i class="fa-brands fa-github text-lg"></i>
        </a>
        <a
          class="text-on-surface/40 hover:text-secondary transition-all hover:scale-125"
          href="https://drive.google.com/file/d/1jLgM2r7PBa2IKNg_Ok81payeakBsQdUr/view"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="CV/Resume"
        >
          <i class="fa-solid fa-file-lines text-lg"></i>
        </a>
        <a
          class="text-primary hover:text-secondary transition-all hover:scale-125"
          :href="'mailto:' + currentData.personalInfo.email"
          aria-label="Email"
        >
          <i class="fa-solid fa-envelope text-lg"></i>
        </a>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref, onMounted, defineAsyncComponent, computed } from 'vue'
import fullstackData from '@/data/fullstack.json'
import frontendData from '@/data/frontend.json'

// Components
const FullStackSection = defineAsyncComponent(() => import('@/components/FullStackSection.vue'))
const FrontendSection = defineAsyncComponent(() => import('@/components/FrontendSection.vue'))

const isDark = ref(true)
const activeTab = ref<'FullStack' | 'Frontend'>('FullStack')

const currentData = computed(() => (activeTab.value === 'FullStack' ? fullstackData : frontendData))

interface Profile {
  role: string
  specialization: string
  heroBadges: { name: string; color: string }[]
}

const currentProfile = computed<Profile>(() => ({
  role: currentData.value.role,
  specialization: currentData.value.specialization,
  heroBadges: currentData.value.heroBadges,
}))

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme) {
    isDark.value = savedTheme === 'dark'
  } else {
    isDark.value = window.matchMedia('(prefers-color-scheme: dark)').matches
  }
  applyTheme()
})

function applyTheme() {
  document.documentElement.setAttribute('data-theme', isDark.value ? 'dark' : 'light')
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

function toggleTheme() {
  isDark.value = !isDark.value
  applyTheme()
}

function scrollTo(id: string) {
  const el = document.getElementById(id)
  if (el) {
    const headerOffset = 80
    const elementPosition = el.getBoundingClientRect().top
    const offsetPosition = elementPosition + window.pageYOffset - headerOffset

    window.scrollTo({
      top: offsetPosition,
      behavior: 'smooth',
    })
  }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 0.5s ease,
    transform 0.5s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>
