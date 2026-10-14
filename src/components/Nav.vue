<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const scrolled = ref(false)
function handler() { scrolled.value = window.scrollY > 20 }
onMounted(() => window.addEventListener('scroll', handler))
onUnmounted(() => window.removeEventListener('scroll', handler))
</script>

<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :style="{
      background: scrolled ? 'rgba(10,10,10,0.85)' : 'transparent',
      backdropFilter: scrolled ? 'blur(12px)' : 'none',
      borderBottom: scrolled ? '1px solid rgba(255,255,255,0.06)' : 'none',
    }"
  >
    <div class="max-w-6xl mx-auto px-8 py-6 flex items-center justify-between">
      <router-link to="/" class="font-bold text-sm tracking-widest uppercase text-white" style="letter-spacing:0.18em">
        Cristian Pottier
      </router-link>
      <ul class="flex gap-10">
        <li><a href="#about" class="nav-link text-sm text-neutral-400" style="letter-spacing:0.04em">About</a></li>
        <li><a href="#projects" class="nav-link text-sm text-neutral-400" style="letter-spacing:0.04em">Projects</a></li>
        <li><a href="#contact" class="nav-link text-sm text-neutral-400" style="letter-spacing:0.04em">Contact</a></li>
      </ul>
    </div>
  </nav>
</template>
