<template>
  <div class="space-y-32">
    <!-- About Me Section -->
    <section id="about" class="max-w-7xl mx-auto px-8 py-32">
      <div class="glass-card p-12 rounded-3xl relative overflow-hidden text-center md:text-left">
        <div class="absolute top-0 left-0 w-64 h-64 bg-secondary/5 blur-[100px] -translate-x-1/2 -translate-y-1/2"></div>
        <div class="relative z-10 max-w-3xl mx-auto md:mx-0">
          <h2 class="text-secondary font-bold tracking-widest uppercase text-xs mb-6">{{ data.personalInfo.about.subtitle }}</h2>
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
          <h2 class="text-primary font-bold tracking-widest uppercase text-xs mb-4">UI/UX Mastery</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Design Arsenal</h3>
        </div>
        <div class="grid md:grid-cols-2 gap-12">
          <div v-for="category in data.skills" :key="category.category" class="space-y-6">
            <div class="flex items-center gap-3">
              <span class="material-symbols-outlined" :class="category.color">{{ category.icon }}</span>
              <h4 class="font-bold text-on-surface">{{ category.category }}</h4>
            </div>
            <div class="flex flex-wrap gap-2">
              <span v-for="skill in category.items" :key="skill" class="bg-surface-container-high px-4 py-2 rounded-xl text-sm font-medium border border-outline-variant/20">{{ skill }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Libraries Section -->
    <section id="libraries" class="max-w-7xl mx-auto px-8 py-32">
      <div class="flex flex-col md:flex-row justify-between items-end gap-8 mb-20">
        <div class="space-y-4">
          <h2 class="text-secondary font-bold tracking-widest uppercase text-xs">Frontend Ecosystem</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Tools & Frameworks</h3>
        </div>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
        <a v-for="lib in data.libraries" :key="lib.name" :href="lib.url" target="_blank" rel="noopener noreferrer" class="glass-card p-8 rounded-3xl border border-on-surface/5 hover:border-secondary/30 transition-all group block text-center">
          <div class="flex flex-col items-center gap-4">
            <div :class="lib.color" class="w-16 h-16 rounded-2xl flex items-center justify-center text-3xl bg-on-surface/5 group-hover:rotate-12 transition-transform">
              <i :class="lib.icon"></i>
            </div>
            <span class="text-lg font-bold text-on-surface">{{ lib.name }}</span>
            <span class="text-xs text-on-surface-variant opacity-60">{{ lib.category }}</span>
          </div>
        </a>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="max-w-7xl mx-auto px-8 py-32 text-center md:text-left">
      <div class="mb-20">
        <h2 class="text-secondary font-bold tracking-widest uppercase text-xs mb-4">Designer's Showcase</h2>
        <h3 class="text-5xl font-black text-on-surface tracking-tighter">Visual Works</h3>
      </div>
      <div class="grid md:grid-cols-2 gap-12">
        <div v-for="project in data.projects" :key="project.title" @click="openGallery(project, 0)" class="group relative aspect-video overflow-hidden rounded-[2.5rem] bg-surface-container cursor-pointer">
          <img :src="project.images[0]" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110 opacity-60 group-hover:opacity-100" />
          <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent p-10 flex flex-col justify-end translate-y-8 group-hover:translate-y-0 transition-transform">
            <span class="text-secondary font-bold text-xs uppercase">{{ project.brand }}</span>
            <h4 class="text-3xl font-bold text-white mt-2">{{ project.title }}</h4>
            <p class="text-white/70 mt-4 line-clamp-2 opacity-0 group-hover:opacity-100 transition-opacity duration-500">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="bg-surface-container-low py-32 px-8">
      <div class="max-w-4xl mx-auto">
        <div class="mb-20 text-center">
          <h2 class="text-secondary font-bold tracking-widest uppercase text-xs mb-4">The Creative Path</h2>
          <h3 class="text-5xl font-black text-on-surface tracking-tighter">Experience</h3>
        </div>
        <div class="space-y-8">
          <div v-for="exp in data.experiences" :key="exp.company" class="glass-card p-8 rounded-3xl border border-secondary/10 hover:border-secondary/30 transition-colors">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
              <div>
                <h4 class="text-2xl font-bold text-on-surface">{{ exp.role }}</h4>
                <p class="text-secondary font-medium">{{ exp.company }}</p>
              </div>
              <span class="text-sm font-bold text-on-surface-variant">{{ exp.period }}</span>
            </div>
            <ul class="mt-6 space-y-3 text-on-surface-variant">
              <li v-for="ach in exp.achievements" :key="ach" class="flex gap-3">
                <span class="text-secondary">✦</span>
                {{ ach }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact CTA -->
    <section id="contact" class="py-32 px-8 text-center">
      <div class="max-w-4xl mx-auto glass-card p-16 rounded-[4rem] border-2 border-secondary/10 relative overflow-hidden">
        <div class="absolute inset-0 bg-gradient-to-br from-secondary/5 to-transparent"></div>
        <div class="relative z-10 space-y-8">
          <h3 class="text-5xl md:text-6xl font-black text-on-surface tracking-tighter">Love what you see?</h3>
          <p class="text-on-surface-variant text-xl max-w-2xl mx-auto">Let's collaborate to build something stunning and user-centric together.</p>
          <div class="flex flex-wrap justify-center gap-6 pt-8">
            <a class="px-12 py-5 rounded-2xl bg-secondary text-on-secondary font-bold text-xl hover:scale-110 transition-transform shadow-lg shadow-secondary/20" :href="'mailto:' + data.personalInfo.email">Get in Touch</a>
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
import { ref } from 'vue'
import data from '@/data/frontend.json'
import ImageGalleryModal from '@/components/ImageGalleryModal.vue'

interface Project {
  title: string
  images: string[]
  brand: string
  description: string
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
