<template>
  <!-- TopNavBar -->
  <header
    :class="[
      'fixed top-0 w-full z-50 transition-all duration-500',
      scrolledDown
        ? 'bg-background/80 backdrop-blur-2xl shadow-[0_8px_32px_rgba(0,0,0,0.2)]'
        : 'bg-transparent',
    ]"
  >
    <nav class="flex justify-between items-center max-w-7xl mx-auto px-6 md:px-8 h-20">
      <div
        class="text-xl font-bold tracking-tighter font-headline gradient-text cursor-pointer"
        @click="scrollTo('hero')"
      >
        {{ currentData.personalInfo.name }}
      </div>

      <!-- Desktop Nav -->
      <div class="hidden md:flex items-center gap-8">
        <button
          v-for="section in navSections"
          :key="section.id"
          @click="scrollTo(section.id)"
          :class="[
            'nav-link text-sm font-medium transition-colors duration-300',
            activeSection === section.id
              ? 'text-primary active'
              : 'text-on-surface/50 hover:text-on-surface',
          ]"
        >
          {{ section.label }}
        </button>
      </div>

      <div class="flex items-center gap-3">
        <button
          @click="toggleTheme"
          class="w-10 h-10 rounded-xl flex items-center justify-center text-on-surface/50 hover:text-primary hover:bg-primary/10 transition-all duration-300"
          aria-label="Toggle Theme"
        >
          <span class="material-symbols-outlined">{{ isDark ? 'light_mode' : 'dark_mode' }}</span>
        </button>

        <!-- Mobile Hamburger -->
        <button
          @click="mobileMenuOpen = !mobileMenuOpen"
          class="md:hidden w-10 h-10 rounded-xl flex items-center justify-center text-on-surface/50 hover:text-primary hover:bg-primary/10 transition-all duration-300"
          aria-label="Menu"
        >
          <span class="material-symbols-outlined">{{ mobileMenuOpen ? 'close' : 'menu' }}</span>
        </button>

        <a
          class="hidden md:inline-flex items-center gap-2 bg-gradient-to-r from-primary to-primary-container text-on-primary px-5 py-2 rounded-xl font-bold text-sm hover:shadow-[0_0_20px_var(--primary-glow)] hover:scale-[1.02] transition-all duration-300"
          :href="'mailto:' + currentData.personalInfo.email"
        >
          <span class="material-symbols-outlined text-base">mail</span>
          Contact
        </a>
      </div>
    </nav>

    <!-- Mobile Menu Drawer -->
    <Transition name="slide-down">
      <div
        v-if="mobileMenuOpen"
        class="md:hidden bg-background/95 backdrop-blur-2xl border-t border-outline-variant/10 px-6 pb-6 pt-2"
      >
        <div class="flex flex-col gap-1">
          <button
            v-for="section in navSections"
            :key="section.id"
            @click="handleNavClick(section.id)"
            :class="[
              'text-left px-4 py-3 rounded-xl font-medium transition-all duration-300',
              activeSection === section.id
                ? 'bg-primary/10 text-primary'
                : 'text-on-surface/60 hover:bg-surface-container hover:text-on-surface',
            ]"
          >
            {{ section.label }}
          </button>
          <a
            class="mt-2 text-center bg-gradient-to-r from-primary to-primary-container text-on-primary px-5 py-3 rounded-xl font-bold text-sm"
            :href="'mailto:' + currentData.personalInfo.email"
          >
            Contact Me
          </a>
        </div>
      </div>
    </Transition>
  </header>

  <main class="relative overflow-hidden pt-20">
    <!-- Tab Switcher -->
    <div class="max-w-7xl mx-auto px-6 md:px-8 mt-10 md:mt-12 mb-8">
      <div class="flex justify-center">
        <div
          class="inline-flex p-1.5 bg-surface-container-high/80 rounded-2xl border border-outline-variant/15 shadow-xl relative backdrop-blur-xl"
        >
          <!-- Sliding indicator -->
          <div
            class="absolute top-1.5 h-[calc(100%-12px)] rounded-xl transition-all duration-500 ease-[cubic-bezier(0.4,0,0.2,1)]"
            :class="
              activeTab === 'FullStack'
                ? 'left-1.5 w-[calc(50%-6px)] bg-gradient-to-r from-primary to-primary-container'
                : 'left-[calc(50%+3px)] w-[calc(50%-6px)] bg-gradient-to-r from-secondary to-secondary-container'
            "
          ></div>
          <button
            @click="activeTab = 'FullStack'"
            :class="[
              'relative z-10 px-6 md:px-8 py-3 rounded-xl text-sm font-bold transition-all duration-500 flex items-center gap-2',
              activeTab === 'FullStack'
                ? 'text-on-primary'
                : 'text-on-surface/50 hover:text-on-surface',
            ]"
          >
            <span class="material-symbols-outlined text-base">code</span>
            Full Stack Developer
          </button>
          <button
            @click="activeTab = 'Frontend'"
            :class="[
              'relative z-10 px-6 md:px-8 py-3 rounded-xl text-sm font-bold transition-all duration-500 flex items-center gap-2',
              activeTab === 'Frontend'
                ? 'text-on-primary'
                : 'text-on-surface/50 hover:text-on-surface',
            ]"
          >
            <span class="material-symbols-outlined text-base">palette</span>
            Frontend Developer
          </button>
        </div>
      </div>
    </div>

    <!-- Hero Section -->
    <section
      id="hero"
      class="relative min-h-[80vh] flex items-center justify-center px-6 md:px-8 py-20 md:py-24 overflow-hidden"
    >
      <!-- Decorative blobs -->
      <div class="blob blob-1 w-[500px] h-[500px] bg-primary/15 top-[-10%] left-[-5%]"></div>
      <div class="blob blob-2 w-[400px] h-[400px] bg-secondary/10 bottom-[-5%] right-[-5%]"></div>
      <div class="blob blob-3 w-[300px] h-[300px] bg-tertiary/8 top-[50%] left-[50%]"></div>
      <div class="absolute inset-0 hero-gradient opacity-50"></div>

      <div
        class="max-w-7xl mx-auto grid md:grid-cols-2 gap-12 md:gap-16 items-center relative z-10"
      >
        <div class="space-y-8">
          <div class="space-y-5">
            <div
              class="reveal flex items-center gap-2 text-secondary font-medium tracking-widest uppercase text-xs"
            >
              <span class="material-symbols-outlined text-sm">location_on</span>
              {{ currentData.personalInfo.location }}
            </div>
            <h1
              class="reveal delay-100 text-5xl md:text-6xl lg:text-7xl font-black leading-[1.05] tracking-tighter text-on-surface font-headline text-glow"
            >
              {{ currentData.personalInfo.name }}
            </h1>
            <div class="reveal delay-200">
              <p class="text-xl md:text-2xl text-on-surface-variant font-light leading-relaxed">
                <span class="typing-cursor">{{ displayedRole }}</span>
                <span class="text-primary mx-2">·</span>
                {{ currentProfile.specialization }}
              </p>
            </div>
          </div>
          <div class="reveal delay-300 flex flex-wrap gap-3">
            <span
              v-for="badge in currentProfile.heroBadges"
              :key="badge.name"
              :class="badge.color"
              class="px-4 py-1.5 rounded-full text-xs font-bold border backdrop-blur-sm"
            >
              {{ badge.name }}
            </span>
          </div>
          <div class="reveal delay-300 flex flex-col gap-3 text-on-surface-variant">
            <a
              class="flex items-center gap-3 hover:text-primary transition-colors duration-300 group"
              :href="'mailto:' + currentData.personalInfo.email"
            >
              <span
                class="material-symbols-outlined text-primary group-hover:scale-110 transition-transform duration-300"
                >mail</span
              >
              <span class="text-sm md:text-base">{{ currentData.personalInfo.email }}</span>
            </a>
            <a
              class="flex items-center gap-3 hover:text-primary transition-colors duration-300 group"
              :href="'tel:' + currentData.personalInfo.phone"
            >
              <span
                class="material-symbols-outlined text-primary group-hover:scale-110 transition-transform duration-300"
                >call</span
              >
              <span class="text-sm md:text-base">{{ currentData.personalInfo.phone }}</span>
            </a>
          </div>
          <div class="reveal delay-400 flex gap-5">
            <a
              class="w-11 h-11 rounded-xl flex items-center justify-center text-on-surface-variant hover:text-secondary hover:bg-secondary/10 transition-all duration-300 hover:scale-110"
              :href="currentData.personalInfo.linkedin"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="LinkedIn"
            >
              <i class="fa-brands fa-linkedin text-xl"></i>
            </a>
            <a
              class="w-11 h-11 rounded-xl flex items-center justify-center text-on-surface-variant hover:text-secondary hover:bg-secondary/10 transition-all duration-300 hover:scale-110"
              :href="currentData.personalInfo.github"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="GitHub"
            >
              <i class="fa-brands fa-github text-xl"></i>
            </a>
            <a
              class="w-11 h-11 rounded-xl flex items-center justify-center text-on-surface-variant hover:text-secondary hover:bg-secondary/10 transition-all duration-300 hover:scale-110"
              href="https://drive.google.com/file/d/1jLgM2r7PBa2IKNg_Ok81payeakBsQdUr/view"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="CV/Resume"
            >
              <i class="fa-solid fa-file-lines text-xl"></i>
            </a>
          </div>
        </div>

        <!-- Profile Image -->
        <div class="reveal-scale delay-200 relative flex justify-center">
          <div class="relative w-fit h-fit">
            <div class="absolute inset-0 bg-primary/15 blur-[80px] rounded-full scale-125"></div>
            <div class="gradient-ring rounded-[2.5rem] md:rounded-[3rem]">
              <div
                class="relative rounded-[2.5rem] md:rounded-[3rem] overflow-hidden bg-background"
              >
                <img
                  alt="Developer Portrait"
                  class="w-full max-w-[18rem] md:max-w-[24rem] h-auto object-contain hover:scale-105 transition-all duration-700"
                  src="/images/Mypicture.jpg"
                />
              </div>
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

  <!-- Back to Top -->
  <Transition name="fade">
    <button
      v-if="scrolledDown"
      @click="scrollToTop"
      class="fixed bottom-8 right-8 z-40 w-12 h-12 rounded-2xl bg-primary/20 backdrop-blur-xl border border-primary/20 text-primary hover:bg-primary hover:text-on-primary transition-all duration-300 shadow-lg hover:shadow-[0_0_20px_var(--primary-glow)] flex items-center justify-center"
      aria-label="Back to top"
    >
      <span class="material-symbols-outlined">arrow_upward</span>
    </button>
  </Transition>

  <!-- Footer -->
  <footer class="w-full bg-surface transition-colors duration-500">
    <div class="section-divider"></div>
    <div
      class="flex flex-col md:flex-row justify-between items-center py-10 px-6 md:px-8 max-w-7xl mx-auto gap-4"
    >
      <div class="text-lg font-bold font-headline gradient-text">
        {{ currentData.personalInfo.name }}
      </div>
      <p class="text-[0.75rem] font-medium text-on-surface/30 tracking-wider">
        &copy; {{ new Date().getFullYear() }} {{ currentData.personalInfo.name }} &middot; Digital
        Curator
      </p>
      <div class="flex gap-4">
        <a
          class="w-9 h-9 rounded-lg flex items-center justify-center text-on-surface/30 hover:text-secondary hover:bg-secondary/10 transition-all duration-300 hover:scale-110"
          :href="currentData.personalInfo.linkedin"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="LinkedIn"
        >
          <i class="fa-brands fa-linkedin text-base"></i>
        </a>
        <a
          class="w-9 h-9 rounded-lg flex items-center justify-center text-on-surface/30 hover:text-secondary hover:bg-secondary/10 transition-all duration-300 hover:scale-110"
          :href="currentData.personalInfo.github"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="GitHub"
        >
          <i class="fa-brands fa-github text-base"></i>
        </a>
        <a
          class="w-9 h-9 rounded-lg flex items-center justify-center text-on-surface/30 hover:text-secondary hover:bg-secondary/10 transition-all duration-300 hover:scale-110"
          href="https://drive.google.com/file/d/1jLgM2r7PBa2IKNg_Ok81payeakBsQdUr/view"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="CV/Resume"
        >
          <i class="fa-solid fa-file-lines text-base"></i>
        </a>
        <a
          class="w-9 h-9 rounded-lg flex items-center justify-center text-primary/60 hover:text-primary hover:bg-primary/10 transition-all duration-300 hover:scale-110"
          :href="'mailto:' + currentData.personalInfo.email"
          aria-label="Email"
        >
          <i class="fa-solid fa-envelope text-base"></i>
        </a>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, defineAsyncComponent, computed, watch } from 'vue'
import fullstackData from '@/data/fullstack.json'
import frontendData from '@/data/frontend.json'

// Components
const FullStackSection = defineAsyncComponent(() => import('@/components/FullStackSection.vue'))
const FrontendSection = defineAsyncComponent(() => import('@/components/FrontendSection.vue'))

const isDark = ref(true)
const activeTab = ref<'FullStack' | 'Frontend'>('FullStack')
const mobileMenuOpen = ref(false)
const scrolledDown = ref(false)
const activeSection = ref('hero')

const navSections = [
  { id: 'about', label: 'About' },
  { id: 'skills', label: 'Skills' },
  { id: 'libraries', label: 'Libraries' },
  { id: 'projects', label: 'Projects' },
  { id: 'experience', label: 'Experience' },
]

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

// Typing animation
const displayedRole = ref('')
const fullRole = computed(() => currentProfile.value.role)
let typingTimeout: ReturnType<typeof setTimeout> | null = null

function typeText(text: string, index = 0) {
  if (typingTimeout) clearTimeout(typingTimeout)
  if (index <= text.length) {
    displayedRole.value = text.slice(0, index)
    typingTimeout = setTimeout(() => typeText(text, index + 1), 60)
  }
}

watch(
  fullRole,
  (newRole) => {
    displayedRole.value = ''
    typeText(newRole)
  },
  { immediate: false },
)

// Scroll handling
function handleScroll() {
  scrolledDown.value = window.scrollY > 50

  // Scroll spy
  const sections: string[] = ['hero', 'about', 'skills', 'libraries', 'projects', 'experience']
  for (let i = sections.length - 1; i >= 0; i--) {
    const sectionId: string = sections[i]!
    const el = document.getElementById(sectionId)
    if (el) {
      const rect = el.getBoundingClientRect()
      if (rect.top <= 150) {
        activeSection.value = sectionId
        break
      }
    }
  }
}

// Scroll reveal observer
let observer: IntersectionObserver | null = null

function setupScrollReveal() {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed')
        }
      })
    },
    { threshold: 0.1, rootMargin: '0px 0px -50px 0px' },
  )

  document.querySelectorAll('.reveal, .reveal-left, .reveal-right, .reveal-scale').forEach((el) => {
    observer!.observe(el)
  })
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme) {
    isDark.value = savedTheme === 'dark'
  } else {
    isDark.value = window.matchMedia('(prefers-color-scheme: dark)').matches
  }
  applyTheme()

  // Start typing animation
  typeText(fullRole.value)

  // Scroll listener
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()

  // Setup scroll reveal after a brief delay to allow DOM render
  setTimeout(() => {
    setupScrollReveal()
  }, 100)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (observer) observer.disconnect()
  if (typingTimeout) clearTimeout(typingTimeout)
})

// Re-observe elements when tab changes
watch(activeTab, () => {
  mobileMenuOpen.value = false
  setTimeout(() => {
    setupScrollReveal()
    typeText(fullRole.value)
  }, 200)
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

function handleNavClick(id: string) {
  scrollTo(id)
  mobileMenuOpen.value = false
}

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
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

.slide-down-enter-active,
.slide-down-leave-active {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.slide-down-enter-from,
.slide-down-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
