<template>
  <!-- TopNavBar -->
  <header class="fixed top-0 w-full z-50 bg-background/70 backdrop-blur-xl shadow-[0_20px_40px_rgba(0,0,0,0.1)] transition-colors duration-300">
    <nav class="flex justify-between items-center max-w-7xl mx-auto px-8 h-20">
      <div class="text-xl font-bold tracking-tighter text-on-surface">{{ data.personalInfo.name }}</div>
      <div class="hidden md:flex items-center gap-8">
        <button @click="scrollTo('about')" class="text-on-surface/60 hover:text-secondary transition-colors duration-300">About</button>
        <button @click="scrollTo('skills')" class="text-on-surface/60 hover:text-secondary transition-colors duration-300">Skills</button>
        <button @click="scrollTo('libraries')" class="text-on-surface/60 hover:text-secondary transition-colors duration-300">Libraries</button>
        <button @click="scrollTo('projects')" class="text-on-surface/60 hover:text-secondary transition-colors duration-300">Projects</button>
        <button @click="scrollTo('experience')" class="text-on-surface/60 hover:text-secondary transition-colors duration-300">Experience</button>
      </div>
      <div class="flex items-center gap-4">
        <button @click="toggleTheme" class="w-10 h-10 rounded-xl flex items-center justify-center text-on-surface/60 hover:bg-surface-container transition-all" aria-label="Toggle Theme">
          <span class="material-symbols-outlined">{{ isDark ? 'light_mode' : 'dark_mode' }}</span>
        </button>
        <div class="hidden md:flex items-center gap-3 text-on-surface/60">
          <span class="material-symbols-outlined">mail</span>
          <span class="material-symbols-outlined">account_circle</span>
        </div>
        <a class="bg-gradient-to-r from-primary to-primary-container text-on-primary px-6 py-2 rounded-lg font-bold hover:scale-95 transition-transform duration-200" :href="'mailto:' + data.personalInfo.email">Contact</a>
      </div>
    </nav>
  </header>

  <main class="relative overflow-hidden pt-20">
    <!-- Hero Section -->
    <section id="hero" class="relative min-h-[921px] flex items-center justify-center px-8 py-24 overflow-hidden">
      <div class="absolute inset-0 hero-gradient opacity-40"></div>
      <div class="max-w-7xl mx-auto grid md:grid-cols-2 gap-16 items-center relative z-10">
        <div class="space-y-8">
          <div class="space-y-4">
            <div class="flex items-center gap-2 text-secondary font-medium tracking-widest uppercase text-xs">
              <span class="material-symbols-outlined text-sm">location_on</span>
              {{ data.personalInfo.location }}
            </div>
            <h1 class="text-6xl md:text-[3.5rem] font-black leading-[1.1] tracking-tighter text-on-surface text-glow">
              {{ data.personalInfo.name }}
            </h1>
            <p class="text-xl text-on-surface-variant font-light max-w-lg leading-relaxed">
              {{ data.personalInfo.role }} <span class="text-primary mx-2">·</span> {{ data.personalInfo.specialization }}
            </p>
          </div>
          <div class="flex flex-wrap gap-3">
            <span v-for="badge in data.heroBadges" :key="badge.name" :class="badge.color" class="px-4 py-1.5 rounded-full text-xs font-bold border">
              {{ badge.name }}
            </span>
          </div>
          <div class="flex flex-col gap-4 text-on-surface-variant">
            <a class="flex items-center gap-3 hover:text-primary transition-colors group" :href="'mailto:' + data.personalInfo.email">
              <span class="material-symbols-outlined text-primary group-hover:scale-110 transition-transform">mail</span>
              {{ data.personalInfo.email }}
            </a>
            <a class="flex items-center gap-3 hover:text-primary transition-colors group" :href="'tel:' + data.personalInfo.phone">
              <span class="material-symbols-outlined text-primary group-hover:scale-110 transition-transform">call</span>
              {{ data.personalInfo.phone }}
            </a>
          </div>
          <div class="flex gap-6">
            <a class="text-on-surface-variant hover:text-secondary transition-all hover:scale-110" :href="data.personalInfo.linkedin" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
              <i class="fa-brands fa-linkedin text-2xl"></i>
            </a>
            <a class="text-on-surface-variant hover:text-secondary transition-all hover:scale-110" :href="data.personalInfo.github" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
              <i class="fa-brands fa-github text-2xl"></i>
            </a>
          </div>
        </div>
        <div class="relative flex justify-center">
          <div class="relative w-fit h-fit">
            <div class="absolute inset-0 bg-primary/20 blur-3xl rounded-full scale-110"></div>
            <div class="relative rounded-[3rem] overflow-hidden border-2 border-on-surface/10 glass-card">
              <img alt="Developer Portrait" class="w-full max-w-[20rem] md:max-w-[24rem] h-auto object-contain hover:scale-105 transition-all duration-700" src="/images/Mypicture.jpg"/>
            </div>
          </div>
        </div>
      </div>
    </section>

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
        <p class="text-on-surface-variant max-w-md text-lg font-light">
          A selection of industrial-grade projects ranging from E-Invoicing systems to complex Call Center management platforms.
        </p>
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
              <img v-for="img in project.images" :key="img" :src="img" class="h-16 w-full object-cover rounded-lg bg-surface-container-lowest" />
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
  </main>

  <footer class="w-full border-t border-outline-variant/10 bg-background transition-colors duration-300">
    <div class="flex flex-col md:flex-row justify-between items-center py-12 px-8 max-w-7xl mx-auto gap-4">
      <div class="text-lg font-black text-on-surface">{{ data.personalInfo.name }}</div>
      <p class="text-[0.75rem] font-medium text-on-surface/40 tracking-wider">© 2024 {{ data.personalInfo.name }} • Digital Curator</p>
      <div class="flex gap-6">
        <a class="text-on-surface/40 hover:text-secondary transition-all hover:scale-125" :href="data.personalInfo.linkedin" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
          <i class="fa-brands fa-linkedin text-lg"></i>
        </a>
        <a class="text-on-surface/40 hover:text-secondary transition-all hover:scale-125" :href="data.personalInfo.github" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
          <i class="fa-brands fa-github text-lg"></i>
        </a>
        <a class="text-primary hover:text-secondary transition-all hover:scale-125" :href="'mailto:' + data.personalInfo.email" aria-label="Email">
          <i class="fa-solid fa-envelope text-lg"></i>
        </a>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import data from '@/data/portfolio.json'

const isDark = ref(true)

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
      behavior: 'smooth'
    })
  }
}
</script>
