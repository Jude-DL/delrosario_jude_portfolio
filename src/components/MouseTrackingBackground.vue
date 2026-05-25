<template>
  <div class="mouse-tracking-bg">
    <canvas ref="canvasRef" class="network-canvas" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'

interface Props {
  mouseX: number
  mouseY: number
}

const props = defineProps<Props>()

const canvasRef = ref<HTMLCanvasElement | null>(null)
let ctx: CanvasRenderingContext2D | null = null
let rafId: number | null = null

const particles: { x: number; y: number; vx: number; vy: number; size: number }[] = []
const PARTICLE_COUNT = 80
const CONNECT_DISTANCE = 110
const mouse = { x: -9999, y: -9999 }

const resizeCanvas = () => {
  const canvas = canvasRef.value
  if (!canvas) return
  const dpr = Math.max(1, window.devicePixelRatio || 1)
  canvas.width = Math.floor(canvas.clientWidth * dpr)
  canvas.height = Math.floor(canvas.clientHeight * dpr)
  ctx = canvas.getContext('2d')
  if (ctx) ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
}

const initParticles = (w: number, h: number) => {
  particles.length = 0
  for (let i = 0; i < PARTICLE_COUNT; i++) {
    particles.push({
      x: Math.random() * w,
      y: Math.random() * h,
      vx: (Math.random() - 0.5) * 0.6,
      vy: (Math.random() - 0.5) * 0.6,
      size: Math.random() * 1.6 + 0.6,
    })
  }
}

const update = () => {
  const canvas = canvasRef.value
  if (!canvas || !ctx) return
  const w = canvas.clientWidth
  const h = canvas.clientHeight

  // clear
  ctx.clearRect(0, 0, w, h)

  // draw background subtle vignette
  const g = ctx.createLinearGradient(0, 0, w, h)
  g.addColorStop(0, '#030305')
  g.addColorStop(1, '#071018')
  ctx.fillStyle = g
  ctx.fillRect(0, 0, w, h)

  // update particles
  for (let p of particles) {
    // simple movement
    p.x += p.vx
    p.y += p.vy

    // repel/attract to mouse
    const dx = mouse.x - p.x
    const dy = mouse.y - p.y
    const dist = Math.sqrt(dx * dx + dy * dy)
    if (dist < 140) {
      const force = (140 - dist) / 140
      p.vx += (dx / dist) * 0.15 * force
      p.vy += (dy / dist) * 0.15 * force
    }

    // slow down
    p.vx *= 0.98
    p.vy *= 0.98

    // bounds
    if (p.x < -20) p.x = w + 20
    if (p.x > w + 20) p.x = -20
    if (p.y < -20) p.y = h + 20
    if (p.y > h + 20) p.y = -20
  }

  // draw connections
  ctx.lineWidth = 0.9
  for (let i = 0; i < particles.length; i++) {
    const a = particles[i]!
    for (let j = i + 1; j < particles.length; j++) {
      const b = particles[j]!
      const dx = a.x - b.x
      const dy = a.y - b.y
      const d = Math.sqrt(dx * dx + dy * dy)
      if (d < CONNECT_DISTANCE) {
        const alpha = 1 - d / CONNECT_DISTANCE
        ctx.strokeStyle = `rgba(180,190,255,${(alpha * 0.6).toFixed(2)})`
        ctx.beginPath()
        ctx.moveTo(a.x, a.y)
        ctx.lineTo(b.x, b.y)
        ctx.stroke()
      }
    }
  }

  // draw nodes
  for (let p of particles) {
    const rad = p.size
    const glow = ctx.createRadialGradient(p.x, p.y, 0, p.x, p.y, rad * 8)
    glow.addColorStop(0, 'rgba(180,190,255,0.9)')
    glow.addColorStop(0.2, 'rgba(140,150,220,0.45)')
    glow.addColorStop(1, 'rgba(10,12,18,0)')
    ctx.fillStyle = glow
    ctx.beginPath()
    ctx.arc(p.x, p.y, rad * 4, 0, Math.PI * 2)
    ctx.fill()

    ctx.fillStyle = 'rgba(220,230,255,0.95)'
    ctx.beginPath()
    ctx.arc(p.x, p.y, rad, 0, Math.PI * 2)
    ctx.fill()
  }

  rafId = requestAnimationFrame(update)
}

const onMouseMove = () => {
  mouse.x = props.mouseX
  mouse.y = props.mouseY
}

onMounted(() => {
  const canvas = canvasRef.value
  if (!canvas) return
  ctx = canvas.getContext('2d')
  resizeCanvas()
  initParticles(canvas.clientWidth, canvas.clientHeight)
  window.addEventListener('resize', () => {
    resizeCanvas()
    initParticles(canvas.clientWidth, canvas.clientHeight)
  })

  // keep mouse synced from props
  onMouseMove()
  rafId = requestAnimationFrame(update)
})

watch(() => [props.mouseX, props.mouseY], onMouseMove)

onUnmounted(() => {
  if (rafId) cancelAnimationFrame(rafId)
})
</script>

<style scoped>
.mouse-tracking-bg {
  position: fixed;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  background: #060609;
}

.network-canvas {
  width: 100%;
  height: 100%;
  display: block;
}

/* subtle overlay to darken center */
.mouse-tracking-bg:after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse at center, rgba(0,0,0,0) 40%, rgba(0,0,0,0.5) 100%);
  pointer-events: none;
}
</style>
