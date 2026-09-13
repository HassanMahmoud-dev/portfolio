<template>
  <div class="space-y-20 md:space-y-32">
    <!-- About Me Section -->
    <section id="about" class="max-w-7xl mx-auto px-6 md:px-8 py-20 md:py-32">
      <div class="glass-card-gradient p-10 md:p-12 rounded-3xl relative overflow-hidden">
        <div
          class="absolute top-0 left-0 w-72 h-72 bg-primary/5 blur-[120px] -translate-x-1/3 -translate-y-1/3"
        ></div>
        <div
          class="absolute bottom-0 right-0 w-48 h-48 bg-secondary/5 blur-[100px] translate-x-1/3 translate-y-1/3"
        ></div>
        <div class="relative z-10 max-w-3xl">
          <div class="reveal flex items-center gap-3 mb-6">
            <span class="material-symbols-outlined text-primary text-xl">format_quote</span>
            <h2 class="text-primary font-bold tracking-widest uppercase text-xs font-headline">
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
          <h2 class="reveal text-secondary font-bold tracking-widest uppercase text-xs mb-4">
            Technical Proficiency
          </h2>
          <h3
            class="reveal delay-100 text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Artillery of Tech
          </h3>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6 md:gap-8">
          <div
            v-for="(category, catIndex) in data.skills"
            :key="category.category"
            class="reveal glass-card p-6 rounded-2xl group hover:shadow-[var(--shadow-glow)]"
            :class="'delay-' + (catIndex + 1) * 100"
          >
            <div class="flex items-center gap-3 mb-5">
              <div
                class="w-10 h-10 rounded-xl bg-primary/10 flex items-center justify-center group-hover:scale-110 transition-transform duration-300"
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
                class="bg-surface-container-high px-3 py-1.5 rounded-lg text-xs font-medium border border-outline-variant/15 hover:border-primary/30 hover:bg-primary/5 transition-all duration-300 cursor-default"
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
          <h2 class="text-tertiary font-bold tracking-widest uppercase text-xs">
            Frameworks & Libraries
          </h2>
          <h3
            class="text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Library Ecosystem
          </h3>
        </div>
        <p class="text-on-surface-variant max-w-sm text-lg font-light leading-relaxed">
          Harnessing the power of modern libraries to build scalable, high-performance applications.
        </p>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-4 md:gap-6">
        <a
          v-for="(lib, libIndex) in data.libraries"
          :key="lib.name"
          :href="lib.url"
          target="_blank"
          rel="noopener noreferrer"
          class="reveal glass-card p-5 md:p-6 rounded-2xl hover:border-primary/30 hover:-translate-y-1 transition-all duration-400 group block"
          :class="'delay-' + ((libIndex % 6) + 1) * 100"
        >
          <div class="flex flex-col items-center gap-3">
            <div
              :class="lib.color"
              class="w-12 h-12 rounded-xl flex items-center justify-center text-2xl bg-on-surface/5 group-hover:scale-110 group-hover:rotate-3 transition-all duration-300"
            >
              <i :class="lib.icon"></i>
            </div>
            <span class="text-sm font-bold text-on-surface">{{ lib.name }}</span>
            <span
              class="text-[10px] text-on-surface-variant text-center leading-tight opacity-50"
              >{{ lib.category }}</span
            >
          </div>
        </a>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="max-w-7xl mx-auto px-6 md:px-8 py-20 md:py-32">
      <div
        class="reveal flex flex-col md:flex-row justify-between items-start md:items-end gap-6 md:gap-8 mb-16 md:mb-20"
      >
        <div class="space-y-4">
          <h2 class="text-primary font-bold tracking-widest uppercase text-xs">Portfolio</h2>
          <h3
            class="text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Case Studies
          </h3>
        </div>
      </div>
      <div class="grid lg:grid-cols-2 gap-8 md:gap-12">
        <div
          v-for="(project, projIndex) in data.projects"
          :key="project.title"
          class="reveal glass-card rounded-3xl overflow-hidden group hover:shadow-[var(--shadow-glow)]"
          :class="'delay-' + (projIndex + 1) * 100"
        >
          <div class="p-8 space-y-6">
            <div class="flex justify-between items-start">
              <div>
                <span class="text-secondary font-bold text-xs uppercase tracking-widest">{{
                  project.brand
                }}</span>
                <h4 class="text-2xl font-bold text-on-surface mt-2 font-headline">
                  {{ project.title }}
                </h4>
              </div>
              <span
                class="material-symbols-outlined text-on-surface-variant/40 group-hover:text-primary transition-colors duration-300 group-hover:translate-x-1 group-hover:-translate-y-1 transform"
                >open_in_new</span
              >
            </div>
            <p class="text-on-surface-variant leading-relaxed text-sm md:text-base">
              {{ project.description }}
            </p>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="tech in project.techStack"
                :key="tech"
                class="bg-primary/10 px-3 py-1 text-[10px] md:text-[11px] rounded-lg uppercase tracking-wider font-bold text-primary border border-primary/10"
                >{{ tech }}</span
              >
            </div>
            <div class="grid grid-cols-4 gap-2 pt-4 border-t border-outline-variant/10">
              <img
                v-for="(img, index) in project.images"
                :key="img"
                :src="img"
                @click="openGallery(project, index)"
                class="h-16 md:h-20 w-full object-cover rounded-xl bg-surface-container-lowest cursor-pointer hover:scale-105 hover:ring-2 hover:ring-primary/30 transition-all duration-300"
              />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="bg-surface-container-low py-20 md:py-32 px-6 md:px-8">
      <div class="max-w-4xl mx-auto">
        <div class="reveal mb-16 md:mb-20">
          <h2 class="text-primary font-bold tracking-widest uppercase text-xs mb-4">Journey</h2>
          <h3
            class="text-4xl md:text-5xl font-black text-on-surface tracking-tighter font-headline"
          >
            Experience
          </h3>
        </div>
        <div class="space-y-10 md:space-y-12">
          <div
            v-for="(exp, expIndex) in data.experiences"
            :key="exp.company"
            class="reveal relative pl-10 md:pl-12 border-l-2 border-primary/20 group"
            :class="'delay-' + (expIndex + 1) * 100"
          >
            <div class="absolute -left-[9px] top-0">
              <div
                class="w-4 h-4 rounded-full bg-primary ring-4 ring-primary/20 group-hover:scale-125 transition-transform duration-300"
                :class="exp.colorClass"
              ></div>
              <div
                class="absolute inset-0 w-4 h-4 rounded-full bg-primary animate-ping opacity-20"
                :class="exp.colorClass"
              ></div>
            </div>
            <div
              class="glass-card p-6 md:p-8 rounded-2xl space-y-4 hover:shadow-[var(--shadow-glow)] transition-all duration-400"
            >
              <div
                class="flex flex-col md:flex-row md:justify-between items-start md:items-center gap-2"
              >
                <h4 class="text-xl md:text-2xl font-bold text-on-surface font-headline">
                  {{ exp.role }}
                </h4>
                <span
                  class="bg-surface-container-high px-4 py-1 rounded-full text-xs font-bold text-primary whitespace-nowrap"
                  >{{ exp.company }} &middot; {{ exp.period }}</span
                >
              </div>
              <ul class="space-y-3 text-on-surface-variant text-sm md:text-base">
                <li v-for="ach in exp.achievements" :key="ach" class="flex gap-3 items-start">
                  <span class="text-primary mt-1 shrink-0">
                    <span class="material-symbols-outlined text-sm">check_circle</span>
                  </span>
                  {{ ach }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section id="education" class="max-w-7xl mx-auto px-6 md:px-8 py-20 md:py-32">
      <div class="grid md:grid-cols-2 gap-12 md:gap-16 items-center">
        <div class="space-y-6">
          <h2 class="reveal text-tertiary font-bold tracking-widest uppercase text-xs">
            Foundation
          </h2>
          <h3
            class="reveal delay-100 text-4xl md:text-5xl font-bold text-on-surface tracking-tight font-headline"
          >
            Academic Roots
          </h3>
          <p class="reveal delay-200 text-on-surface-variant text-lg leading-relaxed">
            Educational excellence providing the theoretical groundwork for complex systems design
            and architectural planning.
          </p>
        </div>
        <div
          class="reveal-scale delay-200 glass-card-gradient p-8 md:p-10 rounded-3xl relative group"
        >
          <div
            class="absolute -top-8 -right-8 w-28 h-28 bg-tertiary/15 rounded-full blur-2xl group-hover:bg-tertiary/25 transition-colors duration-500"
          ></div>
          <div
            class="absolute -bottom-6 -left-6 w-20 h-20 bg-primary/10 rounded-full blur-xl"
          ></div>
          <div class="relative z-10 space-y-6">
            <div class="flex items-center gap-4">
              <div class="w-14 h-14 rounded-2xl bg-tertiary/10 flex items-center justify-center">
                <span class="material-symbols-outlined text-tertiary text-3xl">{{
                  data.education.icon
                }}</span>
              </div>
              <div>
                <h4 class="text-xl font-bold text-on-surface font-headline">
                  {{ data.education.degree }}
                </h4>
                <p class="text-on-surface-variant text-sm">{{ data.education.institution }}</p>
              </div>
            </div>
            <div class="flex justify-between items-center pt-4 border-t border-on-surface/5">
              <span class="text-on-surface-variant font-medium text-sm"
                >Graduation Year: {{ data.education.year }}</span
              >
              <span class="px-4 py-1.5 rounded-xl bg-tertiary/10 text-tertiary font-bold text-sm">{{
                data.education.grade
              }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact CTA -->
    <section id="contact" class="py-20 md:py-32 px-6 md:px-8 text-center relative overflow-hidden">
      <div
        class="absolute inset-0 bg-gradient-to-b from-surface-container-low via-surface-container to-surface-container-lowest"
      ></div>
      <div class="blob blob-1 w-[400px] h-[400px] bg-primary/10 top-[10%] left-[10%]"></div>
      <div class="blob blob-2 w-[300px] h-[300px] bg-secondary/8 bottom-[10%] right-[10%]"></div>
      <div class="max-w-4xl mx-auto space-y-10 md:space-y-12 relative z-10">
        <h3
          class="reveal text-4xl md:text-5xl lg:text-6xl font-black text-on-surface tracking-tighter font-headline"
        >
          Ready to curate your next project?
        </h3>
        <div class="reveal delay-200 flex flex-wrap justify-center gap-5">
          <a
            class="px-8 md:px-10 py-4 md:py-5 rounded-2xl bg-gradient-to-r from-primary to-primary-container text-on-primary font-bold text-lg md:text-xl hover:shadow-[0_0_30px_var(--primary-glow)] hover:scale-[1.03] transition-all duration-300 flex items-center gap-3"
            :href="'mailto:' + data.personalInfo.email"
          >
            <span class="material-symbols-outlined">mail</span>
            Hire Hassan
          </a>
          <a
            class="px-8 md:px-10 py-4 md:py-5 rounded-2xl bg-surface-container-high border border-outline-variant/20 text-on-surface font-bold text-lg md:text-xl hover:bg-surface-container-highest hover:border-outline-variant/40 transition-all duration-300 flex items-center gap-3"
            :href="'tel:' + data.personalInfo.phone"
          >
            <span class="material-symbols-outlined">call</span>
            Call Now
          </a>
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
import data from '@/data/fullstack.json'
import ImageGalleryModal from '@/components/ImageGalleryModal.vue'

interface Project {
  title: string
  images: string[]
  brand: string
  description: string
  techStack: string[]
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

// Re-observe when component is reactivated
watch(isGalleryOpen, () => {
  if (!isGalleryOpen.value) {
    setTimeout(() => setupScrollReveal(), 100)
  }
})
</script>
