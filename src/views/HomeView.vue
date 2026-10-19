<script setup>
import GridBackground from '../components/GridBackground.vue'
import { projects } from '../data/projects.js'

const skills = ['UI Design', 'UX Design', 'Design System', 'Création visuelle', 'Gestion de projet']
const tools = [
  { name: 'Figma', icon: 'https://cdn.simpleicons.org/figma' },
  { name: 'Photoshop', icon: null },
  { name: 'Premiere Pro', icon: null },
  { name: 'Illustrator', icon: null },
  { name: 'WordPress', icon: 'https://cdn.simpleicons.org/wordpress' },
  { name: 'VS Code', icon: null },
  { name: 'Canva', icon: null },
  { name: 'Vue.js', icon: 'https://cdn.simpleicons.org/vuedotjs' },
  { name: 'JavaScript', icon: 'https://cdn.simpleicons.org/javascript' },
  { name: 'PHP', icon: 'https://cdn.simpleicons.org/php' },
]

function scrollToSection(id) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <section class="relative min-h-screen flex items-center overflow-hidden" style="background:#0A0A0A">
    <GridBackground />
    <div class="relative z-10 max-w-6xl mx-auto px-8 w-full py-32">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 lg:gap-24 items-center">
        <div>
          <p class="text-xs tracking-widest uppercase mb-6 font-mono" style="color:#00E5FF; letter-spacing:0.22em">
            Ouvert aux opportunités
          </p>
          <h1 class="text-6xl lg:text-7xl xl:text-8xl font-black leading-none tracking-tight text-white mb-6" style="line-height:0.95">
            Cristian<br />Pottier.
          </h1>
          <p class="text-xl lg:text-2xl font-light mb-10" style="color:#888888">Ingénieur des médias</p>
          <p class="text-base leading-relaxed max-w-md" style="color:#555555; font-weight:300">
            Diplômé en ingénierie des médias, passionné par le marketing digital et l'UX/UI, je conçois des interfaces qui allient stratégie et expérience utilisateur.
          </p>
          <div class="mt-12 flex gap-6 items-center">
            <a href="#" @click.prevent="scrollToSection('projects')" class="text-sm font-medium px-6 py-3 border border-white text-white transition-all duration-200 hover:bg-white hover:text-black" style="letter-spacing:0.06em">
              Voir mes projets
            </a>
            <a href="#" @click.prevent="scrollToSection('contact')" class="text-sm font-medium transition-colors duration-200 hover:text-white" style="color:#555555; letter-spacing:0.06em">
              Me contacter -&gt;
            </a>
          </div>
        </div>

        <div class="flex justify-center lg:justify-end">
          <div class="avatar-wrap" style="width:clamp(240px, 30vw, 340px); height:clamp(240px, 30vw, 340px); border-radius:50%; overflow:hidden; background:#ffffff">
            <img src="/avatar.png" alt="Cristian Pottier" class="w-full h-full object-contain" style="padding:24px" />
          </div>
        </div>
      </div>
    </div>

    <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 opacity-30">
      <div class="w-px h-10" style="background:linear-gradient(to bottom, transparent, white)"></div>
      <span class="text-xs font-mono tracking-widest" style="color:white; letter-spacing:0.2em">scroll</span>
    </div>
  </section>

  <section id="about" class="min-h-screen flex items-center py-32" style="background:#0A0A0A">
    <div class="max-w-6xl mx-auto px-8">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-20 items-start">
        <div>
          <p class="text-xs tracking-widest uppercase font-mono mb-6" style="color:#00E5FF; letter-spacing:0.2em">À propos</p>
          <h2 class="text-4xl lg:text-5xl font-bold text-white leading-tight mb-8" style="line-height:1.1">
            Le design à la<br />croisée de la forme<br />et de la fonction.
          </h2>
          <p class="text-base leading-relaxed" style="color:#555555; font-weight:300; max-width:38ch">
            Passionné par l'UX/UI, la conception d'interfaces intuitives et la création visuelle appliquée aux produits numériques.
          </p>
        </div>
        <div>
          <p class="text-xs tracking-widest uppercase font-mono mb-6" style="color:#333333; letter-spacing:0.2em">Compétences</p>
          <div class="flex flex-wrap gap-2.5 mb-10">
            <span v-for="skill in skills" :key="skill" class="skill-pill text-xs px-4 py-2 font-mono cursor-default" style="border:1px solid rgba(255,255,255,0.12); color:#888888; letter-spacing:0.04em">
              {{ skill }}
            </span>
          </div>

          <p class="text-xs tracking-widest uppercase font-mono mb-6" style="color:#333333; letter-spacing:0.2em">Outils</p>
          <div class="flex flex-wrap gap-2.5">
            <span
              v-for="tool in tools"
              :key="tool.name"
              class="skill-pill text-xs px-4 py-2 font-mono cursor-default flex items-center gap-2"
              style="border:1px solid rgba(255,255,255,0.12); color:#888888; letter-spacing:0.04em"
            >
              <img v-if="tool.icon" :src="tool.icon" :alt="tool.name" style="width:14px; height:14px; filter:grayscale(1) brightness(1.3); opacity:0.8" />
              {{ tool.name }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="projects" class="py-32" style="background:#0A0A0A; border-top:1px solid rgba(255,255,255,0.05)">
    <div class="max-w-6xl mx-auto px-8">
      <p class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#00E5FF; letter-spacing:0.2em">Travaux sélectionnés</p>
      <h2 class="text-4xl lg:text-5xl font-bold text-white mb-16">Projets</h2>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
        <router-link
          v-for="project in projects"
          :key="project.slug"
          :to="'/projet/' + project.slug"
          class="project-card group cursor-pointer block"
          style="background:#111111; border:1px solid rgba(255,255,255,0.07); border-radius:10px; overflow:hidden"
        >
          <div class="relative overflow-hidden" style="height:200px; background:#111111">
            <img
              v-if="project.images && project.images[0]"
              :src="project.images[0]"
              :alt="project.title"
              class="absolute inset-0 w-full h-full object-cover"
            />
            <div class="absolute inset-0" style="background:linear-gradient(to top, rgba(0,0,0,0.85), rgba(0,0,0,0.15))"></div>
            <div class="absolute inset-0 flex items-end p-6">
              <div class="flex gap-2 flex-wrap">
                <span v-for="tag in project.tags" :key="tag" class="text-xs font-mono px-2.5 py-1" style="background:rgba(0,0,0,0.5); color:#666666; border:1px solid rgba(255,255,255,0.08); border-radius:4px">
                  {{ tag }}
                </span>
              </div>
            </div>
          </div>
          <div class="p-6">
            <p class="text-xs font-mono mb-2" style="color:#00E5FF; letter-spacing:0.1em">{{ project.category }}</p>
            <h3 class="text-base font-semibold text-white mb-2">{{ project.title }}</h3>
            <p class="text-sm leading-relaxed" style="color:#555555; font-weight:300">{{ project.shortDescription }}</p>
            <div class="mt-5 flex items-center gap-1" style="color:#333333">
              <span class="text-xs font-mono tracking-widest">VOIR LE PROJET</span>
              <span class="text-xs transition-transform duration-200 group-hover:translate-x-1">-&gt;</span>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </section>
</template>

<style scoped>
.avatar-wrap {
  animation: float 4s ease-in-out infinite;
  transition: box-shadow 0.4s ease, transform 0.4s ease;
  box-shadow: 0 0 0 rgba(0, 229, 255, 0);
}
.avatar-wrap:hover {
  box-shadow: 0 0 40px rgba(0, 229, 255, 0.35);
  transform: scale(1.03);
}
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-12px); }
}
</style>