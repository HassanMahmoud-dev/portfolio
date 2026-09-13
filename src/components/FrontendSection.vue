<template>
  <div class="space-y-20 md:space-y-32">
    <!-- About Me Section -->
    <section id="about" class="max-w-7xl mx-auto px-6 md:px-8 py-20 md:py-32">
      <div
        class="glass-card-gradient p-10 md:p-12 rounded-3xl relative overflow-hidden text-center md:text-left"
      >
        <div
          class="absolute top-0 left-0 w-72 h-72 bg-secondary/5 blur-[120px] -translate-x-1/3 -translate-y-1/3"
        ></div>
        <div
          class="absolute bottom-0 right-0 w-48 h-48 bg-primary/5 blur-[100px] translate-x-1/3 translate-y-1/3"
        ></div>
        <div class="relative z-10 max-w-3xl mx-auto md:mx-0">
          <div class="reveal flex items-center gap-3 mb-6 justify-center md:justify-start">
            <span class="material-symbols-outlined text-secondary text-xl">format_quote</span>
            <h2 class="text-secondary font-bold tracking-widest uppercase text-xs font-headline">
              {{ data.personalInfo.about.subtitle }}
            </h2>
          </div>
          <h3
            class="reveal delay-100 text-4xl md:text-5xl font-bold text-on-surface mb-8 tracking-tight font-headline"
          >
            {{ data.personalInfo.about.title }}
          </h3>
          <p
            v-for="(param, index) in data.personalInfo.about.paragraphs"
            :key="index"
            class="reveal delay-200 text-lg text-on-surface-variant leading-relaxed mb-6 last:mb-0"
          >
            {{ param }}
          </p>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="bg-surface-container-low py-20 md:py-32 px-6 md:px-8">
      <div class="max-w-7xl mx-auto">
        <div class="mb-16 md:mb-20 text-center">
          <h2 class="reveal text-primary font-bold tracking-widest uppercase text-xs mb-4">
            UI/UX Mastery
          </h2>
          <h3
            class="reveal delay-100 text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Design Arsenal
          </h3>
        </div>
        <div class="grid md:grid-cols-2 gap-6 md:gap-8">
          <div
            v-for="(category, catIndex) in data.skills"
            :key="category.category"
            class="reveal glass-card p-6 md:p-8 rounded-2xl group hover:shadow-[var(--shadow-glow)]"
            :class="'delay-' + (catIndex + 1) * 100"
          >
            <div class="flex items-center gap-3 mb-5">
              <div
                class="w-10 h-10 rounded-xl bg-secondary/10 flex items-center justify-center group-hover:scale-110 transition-transform duration-300"
              >
                <span class="material-symbols-outlined" :class="category.color">{{
                  category.icon
                }}</span>
              </div>
              <h4 class="font-bold text-on-surface font-headline">{{ category.category }}</h4>
            </div>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="skill in category.items"
                :key="skill"
                class="bg-surface-container-high px-4 py-2 rounded-xl text-sm font-medium border border-outline-variant/15 hover:border-secondary/30 hover:bg-secondary/5 transition-all duration-300 cursor-default"
                >{{ skill }}</span
              >
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Libraries Section -->
    <section id="libraries" class="max-w-7xl mx-auto px-6 md:px-8 py-20 md:py-32">
      <div
        class="reveal flex flex-col md:flex-row justify-between items-start md:items-end gap-6 md:gap-8 mb-16 md:mb-20"
      >
        <div class="space-y-4">
          <h2 class="text-secondary font-bold tracking-widest uppercase text-xs">
            Frontend Ecosystem
          </h2>
          <h3
            class="text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Tools & Frameworks
          </h3>
        </div>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 md:gap-6">
        <a
          v-for="(lib, libIndex) in data.libraries"
          :key="lib.name"
          :href="lib.url"
          target="_blank"
          rel="noopener noreferrer"
          class="reveal glass-card p-6 md:p-8 rounded-2xl hover:border-secondary/30 hover:-translate-y-1 transition-all duration-400 group block text-center"
          :class="'delay-' + ((libIndex % 4) + 1) * 100"
        >
          <div class="flex flex-col items-center gap-4">
            <div
              :class="lib.color"
              class="w-14 h-14 md:w-16 md:h-16 rounded-2xl flex items-center justify-center text-2xl md:text-3xl bg-on-surface/5 group-hover:rotate-6 group-hover:scale-110 transition-all duration-300"
            >
              <i :class="lib.icon"></i>
            </div>
            <span class="text-sm md:text-lg font-bold text-on-surface">{{ lib.name }}</span>
            <span class="text-[10px] md:text-xs text-on-surface-variant opacity-50">{{
              lib.category
            }}</span>
          </div>
        </a>
      </div>
    </section>

    <!-- Projects Section -->
    <section
      id="projects"
      class="max-w-7xl mx-auto px-6 md:px-8 py-20 md:py-32 text-center md:text-left"
    >
      <div class="reveal mb-16 md:mb-20">
        <h2 class="text-secondary font-bold tracking-widest uppercase text-xs mb-4">
          Designer's Showcase
        </h2>
        <h3 class="text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline">
          Visual Works
        </h3>
      </div>
      <div class="grid md:grid-cols-2 gap-8 md:gap-12">
        <div
          v-for="(project, projIndex) in data.projects"
          :key="project.title"
          @click="openGallery(project, 0)"
          class="reveal group relative aspect-video overflow-hidden rounded-3xl bg-surface-container cursor-pointer"
          :class="'delay-' + (projIndex + 1) * 100"
        >
          <img
            :src="project.images[0]"
            class="w-full h-full object-cover transition-all duration-700 group-hover:scale-110 opacity-50 group-hover:opacity-80"
          />
          <div
            class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/30 to-transparent p-8 md:p-10 flex flex-col justify-end translate-y-4 group-hover:translate-y-0 transition-transform duration-500"
          >
            <span class="text-secondary font-bold text-xs uppercase tracking-widest">{{
              project.brand
            }}</span>
            <h4 class="text-2xl md:text-3xl font-bold text-white mt-2 font-headline">
              {{ project.title }}
            </h4>
            <p
              class="text-white/60 mt-3 line-clamp-2 opacity-0 group-hover:opacity-100 transition-opacity duration-500 text-sm md:text-base"
            >
              {{ project.description }}
            </p>
            <div
              v-if="project.techStack"
              class="flex flex-wrap gap-2 mt-3 opacity-0 group-hover:opacity-100 transition-opacity duration-500 delay-100"
            >
              <span
                v-for="tech in project.techStack"
                :key="tech"
                class="bg-secondary/20 text-secondary px-2 py-0.5 text-[10px] rounded-md font-bold uppercase"
                >{{ tech }}</span
              >
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="bg-surface-container-low py-20 md:py-32 px-6 md:px-8">
      <div class="max-w-4xl mx-auto">
        <div class="reveal mb-16 md:mb-20 text-center">
          <h2 class="text-secondary font-bold tracking-widest uppercase text-xs mb-4">
            The Creative Path
          </h2>
          <h3
            class="text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Experience
          </h3>
        </div>
        <div class="space-y-6 md:space-y-8">
          <div
            v-for="(exp, expIndex) in data.experiences"
            :key="exp.company"
            class="reveal glass-card p-6 md:p-8 rounded-2xl border-l-4 border-secondary/30 hover:border-secondary transition-all duration-400 hover:shadow-[var(--shadow-glow)]"
            :class="'delay-' + (expIndex + 1) * 100"
          >
            <div
              class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4"
            >
              <div>
                <h4 class="text-xl md:text-2xl font-bold text-on-surface font-headline">
                  {{ exp.role }}
                </h4>
                <p class="text-secondary font-medium text-sm">{{ exp.company }}</p>
              </div>
              <span
                class="text-sm font-bold text-on-surface-variant bg-surface-container-high px-3 py-1 rounded-lg"
                >{{ exp.period }}</span
              >
            </div>
            <ul class="mt-6 space-y-3 text-on-surface-variant text-sm md:text-base">
              <li v-for="ach in exp.achievements" :key="ach" class="flex gap-3 items-start">
                <span class="text-secondary mt-0.5 shrink-0">
                  <span class="material-symbols-outlined text-sm">check_circle</span>
                </span>
                {{ ach }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact CTA -->
    <section id="contact" class="py-20 md:py-32 px-6 md:px-8 relative overflow-hidden">
      <div
        class="max-w-4xl mx-auto glass-card-gradient p-12 md:p-16 rounded-[2rem] md:rounded-[4rem] relative overflow-hidden"
      >
        <div
          class="absolute inset-0 bg-gradient-to-br from-secondary/5 via-transparent to-primary/5"
        ></div>
        <div class="blob blob-1 w-[300px] h-[300px] bg-secondary/8 top-[-10%] right-[-10%]"></div>
        <div class="blob blob-2 w-[200px] h-[200px] bg-primary/6 bottom-[-5%] left-[-5%]"></div>
        <div class="relative z-10 space-y-8 text-center">
          <h3
            class="reveal text-4xl md:text-5xl lg:text-6xl font-black text-on-surface tracking-tighter font-headline"
          >
            Love what you see?
          </h3>
          <p class="reveal delay-100 text-on-surface-variant text-lg md:text-xl max-w-2xl mx-auto">
            Let's collaborate to build something stunning and user-centric together.
          </p>
          <div class="reveal delay-200 flex flex-wrap justify-center gap-5 pt-4">
            <a
              class="px-10 md:px-12 py-4 md:py-5 rounded-2xl bg-secondary text-on-secondary font-bold text-lg md:text-xl hover:shadow-[0_0_30px_rgba(0,210,255,0.2)] hover:scale-[1.03] transition-all duration-300 flex items-center gap-3"
              :href="'mailto:' + data.personalInfo.email"
            >
              <span class="material-symbols-outlined">mail</span>
              Get in Touch
            </a>
          </div>
        </div>
      </div>
    </section>

    <ImageGalleryModal
      :is-open="isGalleryOpen"
      :images="galleryImages"
      :start-index="galleryStartIndex"
      :title="galleryTitle"
      @close="isGalleryOpen = false"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'
import data from '@/data/frontend.json'
import ImageGalleryModal from '@/components/ImageGalleryModal.vue'

interface Project {
  title: string
  images: string[]
  brand: string
  description: string
  techStack?: string[]
}

const isGalleryOpen = ref(false)
const galleryImages = ref<string[]>([])
const galleryStartIndex = ref(0)
const galleryTitle = ref('')

function openGallery(project: Project, index: number) {
  galleryImages.value = project.images
  galleryStartIndex.value = index
  galleryTitle.value = project.title
  isGalleryOpen.value = true
}

// Scroll reveal
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
  setTimeout(() => setupScrollReveal(), 100)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})

watch(isGalleryOpen, () => {
  if (!isGalleryOpen.value) {
    setTimeout(() => setupScrollReveal(), 100)
  }
})
</script>
