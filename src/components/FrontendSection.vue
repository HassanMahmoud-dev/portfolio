<template>
  <div class="divide-y divide-outline-variant/60">
    <!-- 01 / Frontend Overview -->
    <section id="about" class="max-w-6xl mx-auto px-6 md:px-8 py-20 md:py-28">
      <div class="grid lg:grid-cols-12 gap-10 lg:gap-12 items-start">
        <div class="lg:col-span-4 space-y-3 reveal">
          <span class="section-index">01 / Overview</span>
          <h2 class="text-2xl md:text-3xl font-bold text-on-surface tracking-tight">
            {{ data.personalInfo.about.subtitle }}
          </h2>
          <p class="text-xs font-mono text-on-surface-variant">
            Component Systems · State · Accessibility
          </p>
        </div>

        <div class="lg:col-span-8 space-y-6">
          <h3
            class="reveal delay-100 text-2xl sm:text-3xl md:text-4xl font-semibold text-on-surface leading-snug tracking-tight"
          >
            {{ data.personalInfo.about.title }}
          </h3>
          <div class="space-y-4">
            <p
              v-for="(param, index) in data.personalInfo.about.paragraphs"
              :key="index"
              class="reveal delay-200 text-base md:text-lg text-on-surface-variant leading-relaxed"
            >
              {{ param }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- 02 / Frontend Case Studies -->
    <section id="projects" class="max-w-6xl mx-auto px-6 md:px-8 py-20 md:py-28">
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-14 gap-4 reveal">
        <div class="space-y-3">
          <span class="section-index">02 / Selected Work</span>
          <h2 class="text-3xl md:text-4xl font-bold text-on-surface tracking-tight">
            Interface Case Studies
          </h2>
        </div>
        <p class="text-sm text-on-surface-variant max-w-md">
          Focused frontend architecture and UI modernization projects. Click any preview to inspect full-resolution screens.
        </p>
      </div>

      <div class="space-y-10">
        <article
          v-for="(project, projIndex) in data.projects"
          :key="project.title"
          class="reveal surface-card rounded-2xl overflow-hidden transition-all duration-300"
        >
          <div class="grid lg:grid-cols-12 gap-0">
            <!-- Project Narrative (5 cols) -->
            <div class="lg:col-span-5 p-7 md:p-9 flex flex-col justify-between border-b lg:border-b-0 lg:border-r border-outline-variant/60">
              <div class="space-y-5">
                <div class="flex items-center justify-between gap-2">
                  <span class="font-mono text-xs text-primary">
                    0{{ projIndex + 1 }} — {{ project.brand }}
                  </span>
                  <span class="font-mono text-[11px] text-on-surface-variant px-2 py-0.5 rounded bg-surface-container-high">
                    {{ project.images.length }} screens
                  </span>
                </div>

                <h3 class="text-2xl font-bold text-on-surface tracking-tight leading-snug">
                  {{ project.title }}
                </h3>

                <p class="text-sm md:text-base text-on-surface-variant leading-relaxed">
                  {{ project.description }}
                </p>
              </div>

              <div class="pt-8 space-y-5">
                <div v-if="project.techStack">
                  <div class="font-mono text-[10px] uppercase tracking-wider text-on-surface-variant mb-2">
                    UI Stack
                  </div>
                  <div class="flex flex-wrap gap-1.5">
                    <span
                      v-for="tech in project.techStack"
                      :key="tech"
                      class="px-2.5 py-1 text-xs font-mono rounded-md bg-surface-container-high text-on-surface border border-outline-variant"
                    >
                      {{ tech }}
                    </span>
                  </div>
                </div>

                <button
                  @click="openGallery(project, 0)"
                  class="inline-flex items-center gap-2 text-xs font-mono font-medium text-primary hover:underline underline-offset-4 cursor-pointer pt-1"
                >
                  <span>Inspect interface screenshots</span>
                  <span class="material-symbols-outlined text-[16px]">open_in_full</span>
                </button>
              </div>
            </div>

            <!-- Visual Gallery Preview (7 cols) -->
            <div class="lg:col-span-7 bg-surface-container-low p-5 md:p-7 flex flex-col justify-between gap-4">
              <div
                @click="openGallery(project, 0)"
                class="relative rounded-xl overflow-hidden border border-outline-variant bg-surface-container-lowest aspect-[16/10] cursor-pointer group"
              >
                <img
                  :src="project.images[0]"
                  :alt="project.title"
                  class="w-full h-full object-cover object-top group-hover:scale-[1.02] transition-transform duration-500"
                />
                <div
                  class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-colors duration-300 flex items-end justify-end p-3"
                >
                  <span
                    class="opacity-0 group-hover:opacity-100 transition-opacity duration-200 bg-background/90 backdrop-blur-md text-on-surface font-mono text-xs px-3 py-1.5 rounded-lg border border-outline-variant flex items-center gap-1.5"
                  >
                    <span class="material-symbols-outlined text-[15px]">zoom_in</span>
                    View Fullscreen
                  </span>
                </div>
              </div>

              <div v-if="project.images.length > 1" class="grid grid-cols-4 gap-2.5">
                <button
                  v-for="(img, index) in project.images"
                  :key="img"
                  @click="openGallery(project, index)"
                  class="relative h-14 sm:h-16 rounded-lg overflow-hidden border border-outline-variant bg-surface-container-lowest hover:border-primary transition-all cursor-pointer group"
                >
                  <img
                    :src="img"
                    :alt="`${project.title} screen ${index + 1}`"
                    class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300"
                  />
                </button>
              </div>
            </div>
          </div>
        </article>
      </div>
    </section>

    <!-- 03 / Frontend Skills & Ecosystem -->
    <section id="skills" class="max-w-6xl mx-auto px-6 md:px-8 py-20 md:py-28">
      <div class="space-y-3 mb-14 reveal">
        <span class="section-index">03 / Frontend Stack</span>
        <h2 class="text-3xl md:text-4xl font-bold text-on-surface tracking-tight">
          UI Engineering &amp; Tools
        </h2>
      </div>

      <div class="grid md:grid-cols-2 gap-6 mb-12">
        <div
          v-for="(category, catIndex) in data.skills"
          :key="category.category"
          class="reveal surface-card p-7 rounded-2xl"
          :class="'delay-' + (catIndex + 1) * 100"
        >
          <div class="flex items-center justify-between mb-5">
            <div class="flex items-center gap-3">
              <span class="material-symbols-outlined text-[20px]" :class="category.color">
                {{ category.icon }}
              </span>
              <h3 class="text-lg font-bold text-on-surface">{{ category.category }}</h3>
            </div>
            <span class="font-mono text-xs text-on-surface-variant">0{{ catIndex + 1 }}</span>
          </div>

          <div class="flex flex-wrap gap-2 pt-3 border-t border-outline-variant/60">
            <span
              v-for="skill in category.items"
              :key="skill"
              class="bg-surface-container-high px-3 py-1.5 rounded-lg text-xs font-mono text-on-surface border border-outline-variant"
            >
              {{ skill }}
            </span>
          </div>
        </div>
      </div>

      <div id="libraries" class="reveal pt-4">
        <div class="font-mono text-xs uppercase tracking-wider text-on-surface-variant mb-4">
          Core Frontend Ecosystem
        </div>
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-3">
          <a
            v-for="lib in data.libraries"
            :key="lib.name"
            :href="lib.url"
            target="_blank"
            rel="noopener noreferrer"
            class="surface-card px-4 py-3.5 rounded-xl flex items-center gap-3 hover:-translate-y-0.5 transition-all group"
          >
            <div
              :class="lib.color"
              class="w-8 h-8 rounded-lg bg-surface-container-high flex items-center justify-center text-base shrink-0"
            >
              <i :class="lib.icon"></i>
            </div>
            <div class="min-w-0">
              <div class="text-xs font-semibold text-on-surface truncate group-hover:text-primary transition-colors">
                {{ lib.name }}
              </div>
              <div class="font-mono text-[10px] text-on-surface-variant truncate">
                {{ lib.category }}
              </div>
            </div>
          </a>
        </div>
      </div>
    </section>

    <!-- 04 / Experience & Education -->
    <section id="experience" class="max-w-6xl mx-auto px-6 md:px-8 py-20 md:py-28">
      <div class="grid lg:grid-cols-12 gap-12 items-start">
        <div class="lg:col-span-7 space-y-8">
          <div class="space-y-3 reveal">
            <span class="section-index">04 / Experience</span>
            <h2 class="text-3xl font-bold text-on-surface tracking-tight">
              Frontend Career Path
            </h2>
          </div>

          <div class="space-y-6">
            <div
              v-for="exp in data.experiences"
              :key="exp.company"
              class="reveal surface-card p-7 rounded-2xl space-y-5"
            >
              <div class="flex flex-wrap justify-between items-start gap-2 pb-4 border-b border-outline-variant/60">
                <div>
                  <h3 class="text-xl font-bold text-on-surface">{{ exp.role }}</h3>
                  <p class="text-sm font-medium text-primary mt-0.5">{{ exp.company }}</p>
                </div>
                <span class="font-mono text-xs px-3 py-1 rounded-md bg-surface-container-high text-on-surface-variant border border-outline-variant">
                  {{ exp.period }}
                </span>
              </div>

              <ul class="space-y-3 text-sm md:text-base text-on-surface-variant">
                <li v-for="ach in exp.achievements" :key="ach" class="flex gap-3 items-start leading-relaxed">
                  <span class="font-mono text-xs text-primary mt-1 shrink-0">&rarr;</span>
                  <span>{{ ach }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>

        <div id="education" class="lg:col-span-5 space-y-8">
          <div class="space-y-3 reveal">
            <span class="section-index">05 / Education</span>
            <h2 class="text-3xl font-bold text-on-surface tracking-tight">
              Academic Foundation
            </h2>
          </div>

          <div class="reveal surface-card p-7 rounded-2xl space-y-6">
            <div class="flex items-start gap-4">
              <div class="w-11 h-11 rounded-xl bg-surface-container-high border border-outline-variant flex items-center justify-center shrink-0">
                <span class="material-symbols-outlined text-primary text-xl">
                  {{ data.education.icon }}
                </span>
              </div>
              <div>
                <h3 class="text-lg font-bold text-on-surface leading-snug">
                  {{ data.education.degree }}
                </h3>
                <p class="text-sm text-on-surface-variant mt-1">
                  {{ data.education.institution }}
                </p>
              </div>
            </div>

            <div class="flex items-center justify-between pt-4 border-t border-outline-variant/60 font-mono text-xs">
              <span class="text-on-surface-variant">Class of {{ data.education.year }}</span>
              <span class="px-2.5 py-1 rounded bg-surface-container-high text-primary border border-outline-variant">
                {{ data.education.grade }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 06 / Contact CTA -->
    <section id="contact" class="max-w-6xl mx-auto px-6 md:px-8 py-20 md:py-28">
      <div class="reveal surface-card rounded-2xl p-8 md:p-14 flex flex-col lg:flex-row items-start lg:items-center justify-between gap-8">
        <div class="space-y-3 max-w-xl">
          <span class="section-index">06 / Next Steps</span>
          <h2 class="text-3xl md:text-4xl font-bold text-on-surface tracking-tight">
            Need a frontend engineer who cares about clarity and structure?
          </h2>
          <p class="text-sm md:text-base text-on-surface-variant leading-relaxed">
            Let’s collaborate to build responsive, maintainable interfaces for your product.
          </p>
        </div>

        <div class="flex flex-wrap items-center gap-3 shrink-0">
          <a
            class="px-6 py-3 rounded-lg bg-primary text-on-primary font-medium text-sm hover:opacity-95 transition-opacity flex items-center gap-2"
            :href="'mailto:' + data.personalInfo.email"
          >
            <span class="material-symbols-outlined text-[18px]">mail</span>
            <span>{{ data.personalInfo.email }}</span>
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
