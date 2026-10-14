<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const canvasRef = ref(null)
let mouse = { x: -9999, y: -9999 }
let raf = 0
let ctx = null

function resize() {
  const canvas = canvasRef.value
  canvas.width = canvas.offsetWidth
  canvas.height = canvas.offsetHeight
}

function onMove(e) {
  const rect = canvasRef.value.getBoundingClientRect()
  mouse = { x: e.clientX - rect.left, y: e.clientY - rect.top }
}

function draw() {
  const canvas = canvasRef.value
  if (!canvas || !ctx) return
  ctx.clearRect(0, 0, canvas.width, canvas.height)
  const gap = 40
  const cols = Math.ceil(canvas.width / gap) + 1
  const rows = Math.ceil(canvas.height / gap) + 1

  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      const x = i * gap
      const y = j * gap
      const dx = x - mouse.x
      const dy = y - mouse.y
      const dist = Math.sqrt(dx * dx + dy * dy)
      const radius = 160
      const proximity = Math.max(0, 1 - dist / radius)
      const baseAlpha = 0.07
      const alpha = baseAlpha + proximity * 0.28
      const size = 1 + proximity * 2.5

      ctx.beginPath()
      ctx.arc(x, y, size, 0, Math.PI * 2)
      ctx.fillStyle = proximity > 0.05
        ? `rgba(0, 229, 255, ${alpha})`
        : `rgba(255, 255, 255, ${baseAlpha})`
      ctx.fill()
    }
  }
  raf = requestAnimationFrame(draw)
}

onMounted(() => {
  ctx = canvasRef.value.getContext('2d')
  resize()
  window.addEventListener('resize', resize)
  window.addEventListener('mousemove', onMove)
  draw()
})

onUnmounted(() => {
  window.removeEventListener('resize', resize)
  window.removeEventListener('mousemove', onMove)
  cancelAnimationFrame(raf)
})
</script>

<template>
  <canvas ref="canvasRef" class="absolute inset-0 w-full h-full pointer-events-none"></canvas>
</template>
