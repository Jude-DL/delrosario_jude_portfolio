<template>
  <div class="mouse-tracking-bg">
    <!-- Starfield -->
    <div class="starfield"></div>
    
    <!-- Galaxy Nebula Clouds -->
    <div class="nebula nebula-1"></div>
    <div class="nebula nebula-2"></div>
    <div class="nebula nebula-3"></div>
    <div class="nebula nebula-4"></div>
    <div class="nebula nebula-5"></div>
    
    <!-- Floating Particles -->
    <div class="particle-container">
      <div v-for="i in 15" :key="i" class="particle" :style="getParticleStyle()"></div>
    </div>
    
    <!-- Cursor-Following Galaxy Orbs -->
    <div 
      class="galaxy-orb orb-1" 
      :style="{ 
        left: blob1X + 'px', 
        top: blob1Y + 'px'
      }"
    ></div>
    <div 
      class="galaxy-orb orb-2" 
      :style="{ 
        left: blob2X + 'px', 
        top: blob2Y + 'px'
      }"
    ></div>
    <div 
      class="galaxy-orb orb-3" 
      :style="{ 
        left: blob3X + 'px', 
        top: blob3Y + 'px'
      }"
    ></div>
    
    <!-- Dark Vignette Overlay -->
    <div class="vignette-overlay"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Props {
  mouseX: number
  mouseY: number
}

const props = defineProps<Props>()

const blob1X = ref(0)
const blob1Y = ref(0)
const blob2X = ref(0)
const blob2Y = ref(0)
const blob3X = ref(0)
const blob3Y = ref(0)
const isMobile = ref(false)

// Helper function to generate particle styles
const getParticleStyle = () => {
  const randomX = Math.random() * 100
  const randomY = Math.random() * 100
  const size = Math.random() * 3 + 1
  const duration = Math.random() * 15 + 10
  const delay = Math.random() * 5
  
  return {
    left: randomX + '%',
    top: randomY + '%',
    width: size + 'px',
    height: size + 'px',
    animationDuration: duration + 's',
    animationDelay: delay + 's',
  }
}

const checkMobile = () => {
  isMobile.value = window.innerWidth <= 768
}

// Smooth interpolation for blob movement
const lerp = (start: number, end: number, factor: number) => {
  return start + (end - start) * factor
}

let animationFrameId: number | null = null

// Continuous animation loop
const animate = () => {
  // Skip mouse interaction on mobile
  if (isMobile.value) {
    animationFrameId = requestAnimationFrame(animate)
    return
  }
  
  // Calculate distance from mouse to each orb
  const dist1 = Math.sqrt(
    Math.pow(props.mouseX - blob1X.value, 2) + Math.pow(props.mouseY - blob1Y.value, 2)
  )
  const dist2 = Math.sqrt(
    Math.pow(props.mouseX - blob2X.value, 2) + Math.pow(props.mouseY - blob2Y.value, 2)
  )
  const dist3 = Math.sqrt(
    Math.pow(props.mouseX - blob3X.value, 2) + Math.pow(props.mouseY - blob3Y.value, 2)
  )
  
  const interactionRange = 250 // Distance at which orbs start reacting to mouse
  
  // Orb 1 - attracts to mouse if within range
  if (dist1 < interactionRange) {
    blob1X.value = lerp(blob1X.value, props.mouseX, 0.08)
    blob1Y.value = lerp(blob1Y.value, props.mouseY, 0.08)
  }
  
  // Orb 2 - attracts to mouse if within range
  if (dist2 < interactionRange) {
    blob2X.value = lerp(blob2X.value, props.mouseX - 80, 0.06)
    blob2Y.value = lerp(blob2Y.value, props.mouseY + 80, 0.06)
  }
  
  // Orb 3 - attracts to mouse if within range
  if (dist3 < interactionRange) {
    blob3X.value = lerp(blob3X.value, props.mouseX + 80, 0.07)
    blob3Y.value = lerp(blob3Y.value, props.mouseY - 80, 0.07)
  }
  
  animationFrameId = requestAnimationFrame(animate)
}

// Initialize blob positions at random locations on screen
onMounted(() => {
  checkMobile()
  window.addEventListener('resize', checkMobile)
  
  blob1X.value = Math.random() * window.innerWidth
  blob1Y.value = Math.random() * window.innerHeight
  blob2X.value = Math.random() * window.innerWidth
  blob2Y.value = Math.random() * window.innerHeight
  blob3X.value = Math.random() * window.innerWidth
  blob3Y.value = Math.random() * window.innerHeight
  
  animate()
})

// Clean up animation loop
onUnmounted(() => {
  window.removeEventListener('resize', checkMobile)
  if (animationFrameId !== null) {
    cancelAnimationFrame(animationFrameId)
  }
})
</script>

<style scoped>
.mouse-tracking-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  overflow: hidden;
  background: radial-gradient(ellipse at center, #0a0515 0%, #050208 50%, #000000 100%);
  pointer-events: none;
}

/* Starfield */
.starfield {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(1px 1px at 20% 30%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 60% 70%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1.5px 1.5px at 50% 50%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 80% 10%, white, rgba(255, 255, 255, 0)),
    radial-gradient(2px 2px at 90% 60%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 30% 80%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 10% 90%, white, rgba(255, 255, 255, 0)),
    radial-gradient(2px 2px at 40% 40%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 70% 20%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1.5px 1.5px at 15% 60%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 85% 75%, white, rgba(255, 255, 255, 0)),
    radial-gradient(2px 2px at 25% 15%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 45% 85%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 75% 45%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1.5px 1.5px at 35% 35%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 65% 65%, white, rgba(255, 255, 255, 0)),
    radial-gradient(2px 2px at 10% 10%, white, rgba(255, 255, 255, 0)),
    radial-gradient(1px 1px at 95% 85%, white, rgba(255, 255, 255, 0));
  background-repeat: repeat;
  background-size: 200% 200%;
  animation: twinkleStar 8s ease-in-out infinite, floatStars 20s ease-in-out infinite;
  opacity: 0.9;
}

@keyframes twinkleStar {
  0%, 100% { opacity: 0.9; }
  50% { opacity: 0.4; }
}

@keyframes floatStars {
  0%, 100% { transform: translateY(0) translateX(0); }
  25% { transform: translateY(-20px) translateX(10px); }
  50% { transform: translateY(-40px) translateX(-15px); }
  75% { transform: translateY(-20px) translateX(10px); }
}

/* Nebula Clouds */
.nebula {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.4;
  mix-blend-mode: screen;
  pointer-events: none;
}

.nebula-1 {
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(168, 85, 247, 0.6) 0%, rgba(168, 85, 247, 0.2) 40%, transparent 70%);
  top: 10%;
  left: 20%;
  animation: floatNebula 20s ease-in-out infinite;
}

.nebula-2 {
  width: 800px;
  height: 800px;
  background: radial-gradient(circle, rgba(99, 102, 241, 0.5) 0%, rgba(99, 102, 241, 0.15) 40%, transparent 70%);
  top: 30%;
  right: 15%;
  animation: floatNebula 25s ease-in-out infinite reverse;
  animation-delay: -5s;
}

.nebula-3 {
  width: 450px;
  height: 450px;
  background: radial-gradient(circle, rgba(236, 72, 153, 0.5) 0%, rgba(236, 72, 153, 0.15) 40%, transparent 70%);
  bottom: 10%;
  left: 50%;
  transform: translateX(-50%);
  animation: floatNebula 30s ease-in-out infinite;
  animation-delay: -10s;
}

.nebula-4 {
  width: 480px;
  height: 480px;
  background: radial-gradient(circle, rgba(34, 211, 238, 0.4) 0%, rgba(34, 211, 238, 0.1) 40%, transparent 70%);
  top: 60%;
  left: 10%;
  animation: floatNebula 28s ease-in-out infinite reverse;
  animation-delay: -3s;
}

.nebula-5 {
  width: 520px;
  height: 520px;
  background: radial-gradient(circle, rgba(168, 85, 247, 0.4) 0%, rgba(168, 85, 247, 0.1) 40%, transparent 70%);
  bottom: 20%;
  right: 10%;
  animation: floatNebula 32s ease-in-out infinite;
  animation-delay: -8s;
}

@keyframes floatNebula {
  0%, 100% {
    transform: translateY(0) translateX(0);
  }
  50% {
    transform: translateY(-50px) translateX(30px);
  }
}

/* Dark Vignette Overlay */
.vignette-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at 50% 50%, transparent 0%, rgba(0, 0, 0, 0.6) 100%);
  pointer-events: none;
}

/* Floating Particles */
.particle-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.particle {
  position: absolute;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.8) 0%, rgba(255, 255, 255, 0) 70%);
  border-radius: 50%;
  animation: floatParticle linear infinite;
  opacity: 0.6;
}

@keyframes floatParticle {
  0% {
    transform: translateY(0) translateX(0);
    opacity: 0;
  }
  10% {
    opacity: 0.6;
  }
  90% {
    opacity: 0.6;
  }
  100% {
    transform: translateY(-100vh) translateX(50px);
    opacity: 0;
  }
}

.galaxy-orb {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  will-change: transform;
  mix-blend-mode: screen;
}

.orb-1 {
  width: 140px;
  height: 140px;
  background: conic-gradient(
    from 0deg,
    rgba(168, 85, 247, 0.9) 0deg,
    rgba(99, 102, 241, 0.8) 90deg,
    rgba(236, 72, 153, 0.7) 180deg,
    rgba(168, 85, 247, 0.9) 360deg
  );
  filter: blur(50px);
  opacity: 0.85;
  box-shadow: 0 0 80px rgba(168, 85, 247, 0.6), 0 0 40px rgba(99, 102, 241, 0.4);
  animation: spin 8s linear infinite;
}

.orb-2 {
  width: 100px;
  height: 100px;
  background: conic-gradient(
    from 45deg,
    rgba(99, 102, 241, 0.9) 0deg,
    rgba(236, 72, 153, 0.8) 120deg,
    rgba(168, 85, 247, 0.7) 240deg,
    rgba(99, 102, 241, 0.9) 360deg
  );
  filter: blur(40px);
  opacity: 0.8;
  box-shadow: 0 0 60px rgba(99, 102, 241, 0.5), 0 0 30px rgba(236, 72, 153, 0.3);
  animation: spin 10s linear infinite reverse;
}

.orb-3 {
  width: 120px;
  height: 120px;
  background: conic-gradient(
    from -45deg,
    rgba(236, 72, 153, 0.9) 0deg,
    rgba(168, 85, 247, 0.8) 100deg,
    rgba(99, 102, 241, 0.7) 220deg,
    rgba(236, 72, 153, 0.9) 360deg
  );
  filter: blur(45px);
  opacity: 0.82;
  box-shadow: 0 0 70px rgba(236, 72, 153, 0.5), 0 0 35px rgba(168, 85, 247, 0.4);
  animation: spin 12s linear infinite;
}

@keyframes spin {
  0% { transform: translate(-50%, -50%) rotate(0deg); }
  100% { transform: translate(-50%, -50%) rotate(360deg); }
}
</style>
