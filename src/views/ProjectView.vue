<script setup>
import { computed } from 'vue'
import { projects } from '../data/projects.js'

const props = defineProps({ slug: String })

const project = computed(() => projects.find(p => p.slug === props.slug))
</script>

<template>
  <section class="relative min-h-screen" style="background:#0A0A0A">
    <div class="max-w-4xl mx-auto px-8 pt-40 pb-32">
      <router-link
        to="/"
        class="inline-flex items-center gap-2 text-sm font-mono mb-16 transition-colors duration-200 hover:text-white"
        style="color:#666666; letter-spacing:0.06em"
      >
        &larr; Retour aux projets
      </router-link>

      <template v-if="project">
        <p class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#00E5FF; letter-spacing:0.2em">
          {{ project.category }} &middot; {{ project.year }}
        </p>
        <h1 class="text-4xl lg:text-6xl font-black text-white mb-8" style="line-height:1.05; letter-spacing:-0.02em">
          {{ project.title }}
        </h1>
        <p class="text-lg leading-relaxed mb-16" style="color:#888888; font-weight:300; max-width:55ch">
          {{ project.shortDescription }}
        </p>

        <div v-if="project.images && project.images[0]" class="mb-20">
          <img
            :src="project.images[0]"
            :alt="project.title"
            class="w-full rounded-lg"
            style="border:1px solid rgba(255,255,255,0.08)"
          />
        </div>

        <div class="flex flex-col gap-14 mb-16">
          <div>
            <h2 class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#333333; letter-spacing:0.15em">Contexte</h2>
            <p class="text-base leading-relaxed" style="color:#999999; font-weight:300; max-width:65ch">{{ project.context }}</p>
          </div>

          <div>
            <h2 class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#333333; letter-spacing:0.15em">Mon rôle</h2>
            <p class="text-base leading-relaxed" style="color:#999999; font-weight:300; max-width:65ch">{{ project.role }}</p>
          </div>
        </div>

        <div style="display:grid; grid-template-columns: 2fr 1fr; gap:4rem; margin-bottom:4rem" class="fonctionnalites-outils-row">
          <div v-if="project.features">
            <h2 class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#333333; letter-spacing:0.15em">Fonctionnalités</h2>
            <ul class="flex flex-col gap-2">
              <li v-for="feature in project.features" :key="feature" class="text-base leading-relaxed" style="color:#999999; font-weight:300">
                - {{ feature }}
              </li>
            </ul>
          </div>

          <div>
            <h2 class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#333333; letter-spacing:0.15em">Outils</h2>
            <div class="flex flex-col gap-2.5">
              <span
                v-for="tool in project.tools"
                :key="tool"
                class="text-xs font-mono px-3 py-2 w-fit"
                style="border:1px solid rgba(255,255,255,0.12); color:#888888; letter-spacing:0.03em"
              >
                {{ tool }}
              </span>
            </div>
          </div>
        </div>

        <div class="mb-16">
          <h2 class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#333333; letter-spacing:0.15em">Démarche</h2>
          <ul class="flex flex-col gap-3">
            <li v-for="(step, i) in project.approach" :key="i" class="flex gap-4 text-base" style="color:#999999; font-weight:300">
              <span class="font-mono text-sm" style="color:#00E5FF">{{ String(i + 1).padStart(2, '0') }}</span>
              {{ step }}
            </li>
          </ul>
        </div>

        <div v-if="project.images && project.images[1]" class="mb-20">
          <img
            :src="project.images[1]"
            :alt="project.title"
            class="w-full rounded-lg"
            style="border:1px solid rgba(255,255,255,0.08)"
          />
        </div>

        <div class="mb-16">
          <h2 class="text-xs tracking-widest uppercase font-mono mb-4" style="color:#333333; letter-spacing:0.15em">Résultat</h2>
          <p class="text-base leading-relaxed" style="color:#999999; font-weight:300; max-width:65ch">{{ project.outcome }}</p>
        </div>

        <div class="flex flex-wrap gap-4 mt-20">
          <a
            v-if="project.liveLink"
            :href="project.liveLink"
            target="_blank"
            class="text-sm font-medium px-6 py-3 border border-white text-white transition-all duration-200 hover:bg-white hover:text-black"
            style="letter-spacing:0.06em"
          >
            Voir le site en ligne
          </a>
          <a
            v-if="project.externalLink"
            :href="project.externalLink"
            target="_blank"
            class="text-sm font-medium transition-colors duration-200 hover:text-white"
            style="color:#555555; letter-spacing:0.06em"
          >
            Voir le code source -&gt;
          </a>
        </div>
      </template>

      <template v-else>
        <p class="text-base" style="color:#666666">Projet introuvable.</p>
      </template>
    </div>
  </section>
</template>

<style scoped>
@media (max-width: 767px) {
  .fonctionnalites-outils-row {
    grid-template-columns: 1fr !important;
  }
}
</style>
