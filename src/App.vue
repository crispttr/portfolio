<script setup>
import { watch } from 'vue'
import { useRoute } from 'vue-router'
import Nav from './components/Nav.vue'
import Contact from './components/Contact.vue'

const route = useRoute()
watch(() => route.fullPath, () => window.scrollTo({ top: 0 }))
</script>

<template>
  <div style="background:#0A0A0A; min-height:100vh;">
    <Nav />
    <router-view />
    <Contact />
  </div>
</template>