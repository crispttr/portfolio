<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const scrolled = ref(false)
const open = ref(false)
function handler() { scrolled.value = window.scrollY > 20 }
onMounted(() => window.addEventListener('scroll', handler))
onUnmounted(() => window.removeEventListener('scroll', handler))

const router = useRouter()
const route = useRoute()

function scrollToSection(id) {
  open.value = false
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
      }, 150)
    })
  } else {
    document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :style="{
      background: scrolled || open ? 'rgba(10,10,10,0.95)' : 'transparent',
      backdropFilter: scrolled || open ? 'blur(12px)' : 'none',
      borderBottom: scrolled || open ? '1px solid rgba(255,255,255,0.06)' : 'none',
    }"
  >
    <div class="max-w-6xl mx-auto px-8 py-6 flex items-center justify-between">
      <router-link
        to="/"
        @click="open = false"
        class="font-bold text-sm tracking-widest uppercase text-white whitespace-nowrap"
        style="letter-spacing:0.18em"
      >
        Cristian Pottier
      </router-link>

      <ul class="hidden md:flex gap-10">
        <li><a href="#" @click.prevent="scrollToSection('about')" class="nav-link text-sm text-neutral-400" style="letter-spacing:0.04em">About</a></li>
        <li><a href="#" @click.prevent="scrollToSection('projects')" class="nav-link text-sm text-neutral-400" style="letter-spacing:0.04em">Projects</a></li>
        <li><a href="#" @click.prevent="scrollToSection('contact')" class="nav-link text-sm text-neutral-400" style="letter-spacing:0.04em">Contact</a></li>
      </ul>

      <button
        class="md:hidden text-white p-1"
        aria-label="Menu"
        @click="open = !open"
      >
        <svg v-if="!open" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round">
          <line x1="4" y1="8" x2="20" y2="8" />
          <line x1="4" y1="16" x2="20" y2="16" />
        </svg>
        <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round">
          <line x1="5" y1="5" x2="19" y2="19" />
          <line x1="19" y1="5" x2="5" y2="19" />
        </svg>
      </button>
    </div>

    <ul v-if="open" class="md:hidden flex flex-col gap-6 px-8 pb-8">
      <li><a href="#" @click.prevent="scrollToSection('about')" class="text-base text-neutral-300">About</a></li>
      <li><a href="#" @click.prevent="scrollToSection('projects')" class="text-base text-neutral-300">Projects</a></li>
      <li><a href="#" @click.prevent="scrollToSection('contact')" class="text-base text-neutral-300">Contact</a></li>
    </ul>
  </nav>
</template>