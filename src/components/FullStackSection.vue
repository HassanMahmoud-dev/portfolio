<template>
  <div class="space-y-32">
    <!-- About Me Section -->
    <section id="about" class="max-w-7xl mx-auto px-8 py-32">
      <div class="glass-card p-12 rounded-3xl relative overflow-hidden">
        <div class="absolute top-0 left-0 w-64 h-64 bg-primary/5 blur-[100px] -translate-x-1/2 -translate-y-1/2"></div>
        <div class="relative z-10 max-w-3xl">
          <h2 class="text-primary font-bold tracking-widest uppercase text-xs mb-6">{{ data.personalInfo.about.subtitle }}</h2>
          <h3 class="text-4xl font-bold text-on-surface mb-8 tracking-tight">{{ data.personalInfo.about.title }}</h3>
          <p v-for="(param, index) in data.personalInfo.about.paragraphs" :key="index" class="text-lg text-on-surface-variant leading-relaxed mb-6">
            {{ param }}
          </p>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="bg-surface-container-low py-32 px-8">
      <div class="max-w-7xl mx-auto">
        <div class="mb-20 text-center">
          <h2 class="text-secondary font-bold tracking-widest uppercase text-xs mb-4">Technical Proficiency</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Artillery of Tech</h3>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div v-for="category in data.skills" :key="category.category" class="space-y-6">
            <div class="flex items-center gap-3">
              <span class="material-symbols-outlined" :class="category.color">{{ category.icon }}</span>
              <h4 class="font-bold text-on-surface">{{ category.category }}</h4>
            </div>
            <div class="flex flex-wrap gap-2">
              <span v-for="skill in category.items" :key="skill" class="bg-surface-container-high px-3 py-1.5 rounded-full text-xs font-medium border border-outline-variant/20">{{ skill }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Libraries Section -->
    <section id="libraries" class="max-w-7xl mx-auto px-8 py-32">
      <div class="flex flex-col md:flex-row justify-between items-end gap-8 mb-20">
        <div class="space-y-4">
          <h2 class="text-tertiary font-bold tracking-widest uppercase text-xs">Frameworks & Libraries</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Library Ecosystem</h3>
        </div>
        <p class="text-on-surface-variant max-w-sm text-lg font-light">
          Harnessing the power of modern libraries to build scalable, high-performance applications.
        </p>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-6">
        <a v-for="lib in data.libraries" :key="lib.name" :href="lib.url" target="_blank" rel="noopener noreferrer" class="glass-card p-6 rounded-2xl border border-on-surface/5 hover:border-primary/30 transition-all group block">
          <div class="flex flex-col items-center gap-4">
            <div :class="lib.color" class="w-12 h-12 rounded-xl flex items-center justify-center text-2xl bg-on-surface/5 group-hover:scale-110 transition-transform">
              <i :class="lib.icon"></i>
            </div>
            <span class="text-sm font-bold text-on-surface">{{ lib.name }}</span>
            <span class="text-[10px] text-on-surface-variant text-center leading-tight opacity-60">{{ lib.category }}</span>
          </div>
        </a>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="max-w-7xl mx-auto px-8 py-32">
      <div class="flex flex-col md:flex-row justify-between items-end gap-8 mb-20">
        <div class="space-y-4">
          <h2 class="text-primary font-bold tracking-widest uppercase text-xs">Portfolio</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Case Studies</h3>
        </div>
      </div>
      <div class="grid lg:grid-cols-2 gap-12">
        <div v-for="project in data.projects" :key="project.title" class="glass-card rounded-[2rem] overflow-hidden group">
          <div class="p-8 space-y-6">
            <div class="flex justify-between items-start">
              <div>
                <span class="text-secondary font-bold text-xs uppercase tracking-widest">{{ project.brand }}</span>
                <h4 class="text-2xl font-bold text-on-surface mt-2">{{ project.title }}</h4>
              </div>
              <span class="material-symbols-outlined text-on-surface-variant group-hover:text-primary transition-colors">open_in_new</span>
            </div>
            <p class="text-on-surface-variant leading-relaxed">
              {{ project.description }}
            </p>
            <div class="flex flex-wrap gap-2">
              <span v-for="tech in project.techStack" :key="tech" class="bg-surface-container-highest px-3 py-1 text-[10px] rounded-full uppercase tracking-tighter font-bold">{{ tech }}</span>
            </div>
            <div class="grid grid-cols-4 gap-2 pt-4">
              <img v-for="(img, index) in project.images" :key="img" :src="img" @click="openGallery(project, index)" class="h-16 w-full object-cover rounded-lg bg-surface-container-lowest cursor-pointer hover:scale-105 transition-transform" />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="bg-surface-container-low py-32 px-8">
      <div class="max-w-4xl mx-auto">
        <div class="mb-20">
          <h2 class="text-primary font-bold tracking-widest uppercase text-xs mb-4">Journey</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Experience</h3>
        </div>
        <div class="space-y-12">
          <div v-for="exp in data.experiences" :key="exp.company" class="relative pl-12 border-l-2 border-primary/20 group">
            <div class="absolute -left-[9px] top-0 w-4 h-4 rounded-full bg-primary ring-4 ring-primary/20 group-hover:scale-125 transition-transform" :class="exp.colorClass"></div>
            <div class="glass-card p-8 rounded-2xl space-y-4">
              <div class="flex flex-col md:flex-row md:justify-between items-start md:items-center gap-2">
                <h4 class="text-2xl font-bold text-on-surface">{{ exp.role }}</h4>
                <span class="bg-surface-container-high px-4 py-1 rounded-full text-xs font-bold text-primary">{{ exp.company }} · {{ exp.period }}</span>
              </div>
              <ul class="space-y-3 text-on-surface-variant list-disc pl-4 marker:text-primary">
                <li v-for="ach in exp.achievements" :key="ach">{{ ach }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section id="education" class="max-w-7xl mx-auto px-8 py-32">
      <div class="grid md:grid-cols-2 gap-16 items-center">
        <div class="space-y-6">
          <h2 class="text-tertiary font-bold tracking-widest uppercase text-xs">Foundation</h2>
          <h3 class="text-4xl font-bold text-on-surface tracking-tight">Academic Roots</h3>
          <p class="text-on-surface-variant text-lg leading-relaxed">
            Educational excellence providing the theoretical groundwork for complex systems design and architectural planning.
          </p>
        </div>
        <div class="glass-card p-10 rounded-[2.5rem] relative group border-2 border-tertiary/10">
          <div class="absolute -top-6 -right-6 w-24 h-24 bg-tertiary/20 rounded-full blur-2xl group-hover:bg-tertiary/30 transition-colors"></div>
          <div class="space-y-6">
            <div class="flex items-center gap-4">
              <span class="material-symbols-outlined text-tertiary text-4xl">{{ data.education.icon }}</span>
              <div>
                <h4 class="text-xl font-bold text-on-surface">{{ data.education.degree }}</h4>
                <p class="text-on-surface-variant">{{ data.education.institution }}</p>
              </div>
            </div>
            <div class="flex justify-between items-center pt-4 border-t border-on-surface/5">
              <span class="text-on-surface-variant font-medium">Graduation Year: {{ data.education.year }}</span>
              <span class="px-4 py-1 rounded-full bg-tertiary/10 text-tertiary font-bold">Grade: {{ data.education.grade }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact CTA -->
    <section id="contact" class="py-32 px-8 text-center bg-gradient-to-b from-surface-container-low to-surface-container-lowest">
      <div class="max-w-4xl mx-auto space-y-12">
        <h3 class="text-5xl md:text-6xl font-black text-on-surface tracking-tighter">Ready to curate your next project?</h3>
        <div class="flex flex-wrap justify-center gap-6">
          <a class="px-10 py-5 rounded-2xl bg-gradient-to-r from-primary to-primary-container text-on-primary font-bold text-xl hover:scale-105 transition-transform flex items-center gap-3" :href="'mailto:' + data.personalInfo.email">
            <span class="material-symbols-outlined">mail</span>
            Hire Hassan
          </a>
          <a class="px-10 py-5 rounded-2xl bg-surface-container-high border border-outline-variant/30 text-on-surface font-bold text-xl hover:bg-surface-container-highest transition-colors flex items-center gap-3" :href="'tel:' + data.personalInfo.phone">
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
import { ref } from 'vue'
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
</script>
