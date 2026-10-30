<template>
  <div class="min-h-screen bg-architectural-grid relative">
    <!-- Top Navigation -->
    <header
      :class="[
        'fixed top-0 w-full z-50 transition-all duration-300',
        scrolledDown
          ? 'bg-background/90 backdrop-blur-md border-b border-outline-variant/60'
          : 'bg-transparent',
      ]"
    >
      <nav class="flex justify-between items-center max-w-6xl mx-auto px-6 md:px-8 h-20">
        <!-- Brand / Monogram -->
        <button
          @click="scrollTo('hero')"
          class="group flex items-center gap-3 text-left focus:outline-none cursor-pointer"
        >
          <span
            class="w-8 h-8 rounded-lg bg-surface-container-high border border-outline-variant flex items-center justify-center font-mono text-xs font-medium text-primary group-hover:border-primary/50 transition-colors"
          >
            HM
          </span>
          <div class="flex flex-col">
            <span class="text-sm font-semibold tracking-tight text-on-surface leading-none">
              {{ currentData.personalInfo.name }}
            </span>
            <span class="font-mono text-[10px] text-on-surface-variant mt-1">
              {{ activeTab === 'FullStack' ? 'Full Stack' : 'Frontend' }} · Mid-Level
            </span>
          </div>
        </button>

        <!-- Desktop Navigation Links -->
        <div class="hidden md:flex items-center gap-7">
          <button
            v-for="(section, idx) in navSections"
            :key="section.id"
            @click="scrollTo(section.id)"
            :class="[
              'nav-link text-xs font-medium tracking-wide transition-colors duration-200 cursor-pointer flex items-center gap-1.5 py-1',
              activeSection === section.id
                ? 'text-on-surface active'
                : 'text-on-surface-variant hover:text-on-surface',
            ]"
          >
            <span class="font-mono text-[10px] text-primary/70">0{{ idx + 1 }}</span>
            {{ section.label }}
          </button>
        </div>

        <!-- Actions (Role Switcher, Theme, Contact) -->
        <div class="flex items-center gap-2.5">
          <!-- Compact Role Switcher in Header for quick access -->
          <div
            class="hidden sm:inline-flex p-1 bg-surface-container border border-outline-variant rounded-lg"
            role="tablist"
            aria-label="Engineering Focus"
          >
            <button
              @click="activeTab = 'FullStack'"
              :class="[
                'px-2.5 py-1 rounded-md text-xs font-medium transition-all duration-200 cursor-pointer',
                activeTab === 'FullStack'
                  ? 'bg-primary text-on-primary shadow-xs'
                  : 'text-on-surface-variant hover:text-on-surface',
              ]"
            >
              Full Stack
            </button>
            <button
              @click="activeTab = 'Frontend'"
              :class="[
                'px-2.5 py-1 rounded-md text-xs font-medium transition-all duration-200 cursor-pointer',
                activeTab === 'Frontend'
                  ? 'bg-primary text-on-primary shadow-xs'
                  : 'text-on-surface-variant hover:text-on-surface',
              ]"
            >
              Frontend
            </button>
          </div>

          <button
            @click="toggleTheme"
            class="w-9 h-9 rounded-lg border border-outline-variant bg-surface-container flex items-center justify-center text-on-surface-variant hover:text-on-surface hover:border-outline transition-colors duration-200 cursor-pointer"
            :aria-label="isDark ? 'Switch to light theme' : 'Switch to dark theme'"
            :title="isDark ? 'Light mode' : 'Dark mode'"
          >
            <span class="material-symbols-outlined text-[18px]">{{
              isDark ? 'light_mode' : 'dark_mode'
            }}</span>
          </button>

          <!-- Mobile Hamburger -->
          <button
            @click="mobileMenuOpen = !mobileMenuOpen"
            class="md:hidden w-9 h-9 rounded-lg border border-outline-variant bg-surface-container flex items-center justify-center text-on-surface-variant hover:text-on-surface transition-colors duration-200"
            aria-label="Toggle Menu"
          >
            <span class="material-symbols-outlined text-[18px]">{{
              mobileMenuOpen ? 'close' : 'menu'
            }}</span>
          </button>

          <a
            class="hidden lg:inline-flex items-center gap-2 bg-on-surface text-background px-4 py-2 rounded-lg font-medium text-xs hover:opacity-90 transition-opacity duration-200"
            :href="'mailto:' + currentData.personalInfo.email"
          >
            <span>Get in touch</span>
            <span class="material-symbols-outlined text-[15px]">arrow_outward</span>
          </a>
        </div>
      </nav>

      <!-- Mobile Menu Drawer -->
      <Transition name="slide-down">
        <div
          v-if="mobileMenuOpen"
          class="md:hidden bg-background/95 backdrop-blur-xl border-b border-outline-variant px-6 pb-6 pt-3"
        >
          <!-- Mobile Role Switcher -->
          <div class="flex sm:hidden p-1 bg-surface-container border border-outline-variant rounded-lg mb-4">
            <button
              @click="activeTab = 'FullStack'"
              :class="[
                'flex-1 py-2 rounded-md text-xs font-medium transition-all duration-200',
                activeTab === 'FullStack'
                  ? 'bg-primary text-on-primary'
                  : 'text-on-surface-variant',
              ]"
            >
              Full Stack Focus
            </button>
            <button
              @click="activeTab = 'Frontend'"
              :class="[
                'flex-1 py-2 rounded-md text-xs font-medium transition-all duration-200',
                activeTab === 'Frontend'
                  ? 'bg-primary text-on-primary'
                  : 'text-on-surface-variant',
              ]"
            >
              Frontend Focus
            </button>
          </div>

          <div class="flex flex-col gap-1">
            <button
              v-for="(section, idx) in navSections"
              :key="section.id"
              @click="handleNavClick(section.id)"
              :class="[
                'text-left px-3 py-2.5 rounded-lg text-sm font-medium transition-colors duration-200 flex items-center gap-3',
                activeSection === section.id
                  ? 'bg-surface-container-high text-primary'
                  : 'text-on-surface-variant hover:bg-surface-container hover:text-on-surface',
              ]"
            >
              <span class="font-mono text-xs text-primary/70">0{{ idx + 1 }}</span>
              {{ section.label }}
            </button>
            <a
              class="mt-3 text-center bg-primary text-on-primary px-4 py-2.5 rounded-lg font-medium text-xs"
              :href="'mailto:' + currentData.personalInfo.email"
            >
              Email Me Directly
            </a>
          </div>
        </div>
      </Transition>
    </header>

    <main class="pt-20">
      <!-- Hero Section -->
      <section
        id="hero"
        class="relative max-w-6xl mx-auto px-6 md:px-8 pt-12 pb-20 md:pt-20 md:pb-28"
      >
        <!-- Top Status Bar / Role Lens Switcher -->
        <div
          class="reveal flex flex-wrap items-center justify-between gap-4 pb-8 mb-10 border-b border-outline-variant/60"
        >
          <div class="flex items-center gap-3">
            <span class="relative flex h-2 w-2">
              <span
                class="animate-ping absolute inline-flex h-full w-full rounded-full bg-primary opacity-75"
              ></span>
              <span class="relative inline-flex rounded-full h-2 w-2 bg-primary"></span>
            </span>
            <span class="font-mono text-xs text-on-surface-variant">
              Based in {{ currentData.personalInfo.location }} · Available for new opportunities
            </span>
          </div>

          <div class="flex items-center gap-2 font-mono text-xs text-on-surface-variant">
            <span>Lens:</span>
            <button
              @click="activeTab = 'FullStack'"
              :class="[
                'underline underline-offset-4 cursor-pointer transition-colors',
                activeTab === 'FullStack'
                  ? 'text-primary font-medium'
                  : 'hover:text-on-surface decoration-transparent',
              ]"
            >
              Full-Stack ERP
            </button>
            <span>/</span>
            <button
              @click="activeTab = 'Frontend'"
              :class="[
                'underline underline-offset-4 cursor-pointer transition-colors',
                activeTab === 'Frontend'
                  ? 'text-primary font-medium'
                  : 'hover:text-on-surface decoration-transparent',
              ]"
            >
              Frontend UI
            </button>
          </div>
        </div>

        <div class="grid lg:grid-cols-12 gap-12 lg:gap-10 items-start">
          <!-- Left Editorial Column (8 cols) -->
          <div class="lg:col-span-8 space-y-8">
            <div class="space-y-4">
              <div class="reveal font-mono text-xs uppercase tracking-widest text-primary">
                {{ currentProfile.role }} — {{ currentProfile.specialization }}
              </div>

              <h1
                class="reveal delay-100 text-4xl sm:text-5xl md:text-6xl font-bold tracking-tight text-on-surface leading-[1.12]"
              >
                Crafting dependable
                <span class="font-serif italic font-normal text-primary">enterprise software</span>
                &amp; thoughtful web interfaces.
              </h1>

              <p
                class="reveal delay-200 text-base md:text-lg text-on-surface-variant max-w-2xl leading-relaxed pt-2"
              >
                I’m <strong class="text-on-surface font-medium">{{ currentData.personalInfo.name }}</strong>,
                a software engineer experienced in building full-lifecycle ERP platforms, government
                tax integrations, and real-time operational tools using Vue.js and Node.js.
              </p>
            </div>

            <!-- Technical Focus Pills -->
            <div class="reveal delay-200 flex flex-wrap gap-2">
              <span
                v-for="badge in currentProfile.heroBadges"
                :key="badge.name"
                class="px-3 py-1 rounded-md font-mono text-xs border border-outline-variant bg-surface-container text-on-surface-variant"
              >
                {{ badge.name }}
              </span>
            </div>

            <!-- Primary CTA & Quick Links -->
            <div class="reveal delay-300 flex flex-wrap items-center gap-4 pt-2">
              <button
                @click="scrollTo('projects')"
                class="px-5 py-2.5 rounded-lg bg-primary text-on-primary font-medium text-sm hover:opacity-95 transition-opacity flex items-center gap-2 cursor-pointer"
              >
                <span>Selected Case Studies</span>
                <span class="material-symbols-outlined text-[18px]">arrow_downward</span>
              </button>

              <a
                href="https://drive.google.com/file/d/1jLgM2r7PBa2IKNg_Ok81payeakBsQdUr/view"
                target="_blank"
                rel="noopener noreferrer"
                class="px-5 py-2.5 rounded-lg border border-outline-variant bg-surface-container text-on-surface font-medium text-sm hover:border-outline transition-colors flex items-center gap-2"
              >
                <span class="material-symbols-outlined text-[18px] text-primary">description</span>
                <span>Read Resume / CV</span>
              </a>

              <div class="flex items-center gap-2 ml-auto sm:ml-2">
                <a
                  :href="currentData.personalInfo.github"
                  target="_blank"
                  rel="noopener noreferrer"
                  aria-label="GitHub"
                  class="w-10 h-10 rounded-lg border border-outline-variant bg-surface-container flex items-center justify-center text-on-surface-variant hover:text-on-surface hover:border-outline transition-colors"
                >
                  <i class="fa-brands fa-github text-base"></i>
                </a>
                <a
                  :href="currentData.personalInfo.linkedin"
                  target="_blank"
                  rel="noopener noreferrer"
                  aria-label="LinkedIn"
                  class="w-10 h-10 rounded-lg border border-outline-variant bg-surface-container flex items-center justify-center text-on-surface-variant hover:text-on-surface hover:border-outline transition-colors"
                >
                  <i class="fa-brands fa-linkedin-in text-base"></i>
                </a>
                <a
                  :href="'mailto:' + currentData.personalInfo.email"
                  aria-label="Email"
                  class="w-10 h-10 rounded-lg border border-outline-variant bg-surface-container flex items-center justify-center text-on-surface-variant hover:text-on-surface hover:border-outline transition-colors"
                >
                  <span class="material-symbols-outlined text-[18px]">mail</span>
                </a>
              </div>
            </div>

            <!-- Key Engineering Highlights Bar -->
            <div
              class="reveal delay-400 grid grid-cols-3 gap-4 pt-8 border-t border-outline-variant/60 max-w-xl"
            >
              <div>
                <div class="font-mono text-xl md:text-2xl font-semibold text-on-surface">ERP &amp; B2B</div>
                <div class="text-xs text-on-surface-variant mt-0.5">Core Domain Focus</div>
              </div>
              <div>
                <div class="font-mono text-xl md:text-2xl font-semibold text-on-surface">Vue 3 + Node</div>
                <div class="text-xs text-on-surface-variant mt-0.5">Primary Stack</div>
              </div>
              <div>
                <div class="font-mono text-xl md:text-2xl font-semibold text-on-surface">Production</div>
                <div class="text-xs text-on-surface-variant mt-0.5">ETA, HMS &amp; Real-time</div>
              </div>
            </div>
          </div>

          <!-- Right Portrait Column (4 cols) - Framed like an editorial dossier card -->
          <div class="lg:col-span-4 reveal-scale delay-200">
            <div class="surface-card rounded-2xl p-3 max-w-xs mx-auto lg:max-w-none">
              <div class="relative rounded-xl overflow-hidden bg-surface-container-highest aspect-[4/5]">
                <img
                  alt="Hassan Mahmoud"
                  class="w-full h-full object-cover object-top grayscale-[15%] contrast-[1.02] hover:grayscale-0 transition-all duration-500"
                  src="/images/Mypicture.jpg"
                />
              </div>
              <div class="pt-3 pb-1 px-1 flex items-center justify-between text-xs">
                <div>
                  <p class="font-medium text-on-surface">{{ currentData.personalInfo.name }}</p>
                  <p class="font-mono text-[11px] text-on-surface-variant">
                    {{ currentData.personalInfo.email }}
                  </p>
                </div>
                <a
                  :href="'tel:' + currentData.personalInfo.phone"
                  class="px-2.5 py-1 rounded-md bg-surface-container-high border border-outline-variant font-mono text-[11px] text-primary hover:bg-primary hover:text-on-primary transition-colors"
                >
                  Call
                </a>
              </div>
            </div>
          </div>
        </div>
      </section>

      <div class="max-w-6xl mx-auto px-6 md:px-8">
        <div class="section-divider"></div>
      </div>

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
        class="fixed bottom-6 right-6 z-40 w-10 h-10 rounded-lg bg-surface-container-high border border-outline-variant text-on-surface-variant hover:text-primary hover:border-primary/40 transition-all duration-200 shadow-md flex items-center justify-center cursor-pointer"
        aria-label="Back to top"
      >
        <span class="material-symbols-outlined text-[18px]">arrow_upward</span>
      </button>
    </Transition>

    <!-- Footer -->
    <footer class="w-full border-t border-outline-variant/60 bg-surface/50">
      <div
        class="flex flex-col sm:flex-row justify-between items-center py-8 px-6 md:px-8 max-w-6xl mx-auto gap-4"
      >
        <div class="flex items-center gap-3">
          <span
            class="w-6 h-6 rounded bg-surface-container-high border border-outline-variant flex items-center justify-center font-mono text-[10px] font-medium text-primary"
          >
            HM
          </span>
          <span class="text-xs text-on-surface-variant">
            &copy; {{ new Date().getFullYear() }} {{ currentData.personalInfo.name }}. Built with Vue 3 &amp; TypeScript.
          </span>
        </div>

        <div class="flex items-center gap-5 font-mono text-xs text-on-surface-variant">
          <a
            class="hover:text-primary transition-colors"
            :href="currentData.personalInfo.github"
            target="_blank"
            rel="noopener noreferrer"
          >
            GitHub
          </a>
          <a
            class="hover:text-primary transition-colors"
            :href="currentData.personalInfo.linkedin"
            target="_blank"
            rel="noopener noreferrer"
          >
            LinkedIn
          </a>
          <a
            class="hover:text-primary transition-colors"
            href="https://drive.google.com/file/d/1jLgM2r7PBa2IKNg_Ok81payeakBsQdUr/view"
            target="_blank"
            rel="noopener noreferrer"
          >
            Resume
          </a>
          <a
            class="hover:text-primary transition-colors"
            :href="'mailto:' + currentData.personalInfo.email"
          >
            Email
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, defineAsyncComponent, computed, watch } from 'vue'
import fullstackData from '@/data/fullstack.json'
import frontendData from '@/data/frontend.json'

const FullStackSection = defineAsyncComponent(() => import('@/components/FullStackSection.vue'))
const FrontendSection = defineAsyncComponent(() => import('@/components/FrontendSection.vue'))

const isDark = ref(true)
const activeTab = ref<'FullStack' | 'Frontend'>('FullStack')
const mobileMenuOpen = ref(false)
const scrolledDown = ref(false)
const activeSection = ref('hero')

const navSections = [
  { id: 'about', label: 'Overview' },
  { id: 'projects', label: 'Work' },
  { id: 'skills', label: 'Stack' },
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

function handleScroll() {
  scrolledDown.value = window.scrollY > 40

  const sections: string[] = ['hero', 'about', 'projects', 'skills', 'experience']
  for (let i = sections.length - 1; i >= 0; i--) {
    const sectionId: string = sections[i]!
    const el = document.getElementById(sectionId)
    if (el) {
      const rect = el.getBoundingClientRect()
      if (rect.top <= 160) {
        activeSection.value = sectionId
        break
      }
    }
  }
}

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
    { threshold: 0.1, rootMargin: '0px 0px -40px 0px' },
  )

  document.querySelectorAll('.reveal, .reveal-scale').forEach((el) => {
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

  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()

  setTimeout(() => {
    setupScrollReveal()
  }, 100)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (observer) observer.disconnect()
})

watch(activeTab, () => {
  mobileMenuOpen.value = false
  setTimeout(() => {
    setupScrollReveal()
  }, 150)
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
    opacity 0.35s ease,
    transform 0.35s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.slide-down-enter-active,
.slide-down-leave-active {
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

.slide-down-enter-from,
.slide-down-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>
