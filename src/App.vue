<template>
  <div class="portfolio" @mousemove="handleMouseMove">
    <!-- Animated Background with Mouse Tracking -->
    <MouseTrackingBackground :mouseX="mouseX" :mouseY="mouseY" />
    
    <!-- Navigation -->
    <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
      <div class="nav-content">
        <div class="logo" @click="downloadCV">
          <div class="logo-circle">JD</div>
          <div class="logo-text">My Portfolio</div>
        </div>
        <ul class="nav-links">
          <li><a href="#home" @click="scrollToSection" class="nav-link">Home</a></li>
          <li><a href="#about" @click="scrollToSection" class="nav-link">About</a></li>
          <li><a href="#projects" @click="scrollToSection" class="nav-link">Projects</a></li>
          <li><a href="#skills" @click="scrollToSection" class="nav-link">Skills</a></li>
          <li><a href="#contact" @click="scrollToSection" class="nav-link">Contact</a></li>
        </ul>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="hero-wrapper">
        <div class="hero-content">
          <div class="hero-badge">
            <span class="badge-dot"></span>
            Available for Projects
          </div>
          <h1 class="title">
            <span class="title-word">JUDE</span>
            <span class="title-word">CHRISTIAN</span>
            <span class="title-word highlight">DEL ROSARIO</span>
          </h1>
          <p class="description">Information Technology student skilled in MERN/MEVN stack, Flutter, and network security. Experienced in project coordination, technical leadership, and creating technology-driven solutions.</p>
          <div class="hero-actions">
            <button class="btn-primary" @click="downloadCV">
              Download CV
            </button>
            <button class="btn-secondary" @click="scrollToSection({target: {hash: '#contact'}})">
              Get In Touch
            </button>
          </div>
        </div>
        <div class="hero-3d">
          <div class="profile-image-wrapper">
            <img :src="profileImage" alt="Jude Christian Del Rosario" class="profile-image" />
          </div>
        </div>
      </div>
      <div class="scroll-indicator">
        <div class="scroll-dot"></div>
        <p>Scroll to explore</p>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">About Me</h2>
          <div class="title-underline"></div>
        </div>
        <div class="about-content">
          <div class="about-left">
            <div class="about-card">
              <h3>Who I Am</h3>
              <p>I'm an IT student at Pamantasan ng Cabuyao with proven leadership in research and organizational management. I combine technical proficiency in full-stack development with strong communication and strategic planning abilities.</p>
            </div>
            <div class="about-card">
              <h3>What I Do</h3>
              <p>I specialize in modern web technologies (MERN/MEVN), mobile development with Flutter, and network security. I'm experienced in project coordination, event management, and creating technology-driven solutions that enhance productivity.</p>
            </div>
          </div>
          <div class="about-image">
            <img :src="awardImage" alt="Jude Christian Del Rosario - Award Winner" />
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="projects">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Featured Projects</h2>
          <div class="title-underline"></div>
          <p class="section-subtitle">A selection of projects I've built recently</p>
        </div>
        <div class="projects-grid">
          <ProjectCard 
            v-for="project in projects" 
            :key="project.id"
            :project="project"
          />
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="skills">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Skills & Technologies</h2>
          <div class="title-underline"></div>
          <p class="section-subtitle">Tools and technologies I work with</p>
        </div>
        <div class="skills-grid">
          <div class="skill-category" v-for="category in skillCategories" :key="category.name">
            <h3 class="category-title">{{ category.name }}</h3>
            <div class="skill-tags">
              <span class="skill-tag" v-for="skill in category.skills" :key="skill">
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
      <div class="container">
        <div class="contact-wrapper">
          <div class="contact-header">
            <h2 class="section-title">Let's Work Together</h2>
            <p class="contact-description">Have a project in mind? I'd love to hear from you. Let's create something amazing together.</p>
          </div>
          <div class="contact-links">
            <a href="mailto:delrosariojude61@gmail.com" class="contact-link-card">
              <div class="link-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="2" y="4" width="20" height="16" rx="2"></rect>
                  <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"></path>
                </svg>
              </div>
              <div class="link-content">
                <h4>Email</h4>
                <p>delrosariojude61@gmail.com</p>
              </div>
              <span class="link-arrow">→</span>
            </a>
            <a href="https://www.linkedin.com/in/del-rosario-jude-christian-d-215985386/" class="contact-link-card">
              <div class="link-icon">
                <svg viewBox="0 0 24 24" fill="currentColor">
                  <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.225 0z"></path>
                </svg>
              </div>
              <div class="link-content">
                <h4>LinkedIn</h4>
                <p>Connect with me</p>
              </div>
              <span class="link-arrow">→</span>
            </a>
            <a href="https://github.com/Jude-DL" class="contact-link-card">
              <div class="link-icon">
                <svg viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v 3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"></path>
                </svg>
              </div>
              <div class="link-content">
                <h4>GitHub</h4>
                <p>Check my work</p>
              </div>
              <span class="link-arrow">→</span>
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <p class="footer-text">&copy; 2025 Jude Christian D. Del Rosario.</p>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import MouseTrackingBackground from './components/MouseTrackingBackground.vue'
import ProjectCard from './components/ProjectCard.vue'
import awardImage from './assets/IMG_7603.jpg'
import profileImage from './assets/25f9482b-da02-469d-be6d-51891a4fc50e.png'

const mouseX = ref(0)
const mouseY = ref(0)
const isScrolled = ref(false)

const projects = [
  {
    id: 1,
    title: 'POLICE-NOW',
    description: 'A mobile based real time emergency response and police assistance application.',
    tags: ['Full Stack', 'Web Development', 'Mobile Development'],
    image: new URL('./assets/projects/Black and White Minimalist Elegant Modern Typography  Creative Studio Brand Logo.png', import.meta.url).href,
    link: '#',
  },
  {
    id: 2,
    title: 'MERN User Management System',
    description: 'Full-stack web application built with MongoDB, Express, React, and Node.js. Features real-time data synchronization and responsive design.',
    tags: ['MERN', 'Full Stack', 'JavaScript'],
    image: new URL('./assets/projects/Mern.png', import.meta.url).href,
    link: '#',
  },
  {
    id: 3,
    title: 'Task Management System',
    description: 'A full-stack task management system using Laravel and React. Includes user authentication, task assignment, and progress tracking features.',
    tags: ['Laravel', 'React', 'Full Stack'],
    image: new URL('./assets/projects/Task.png', import.meta.url).href,
    link: '#',
  },
  {
    id: 4,
    title: 'MEVN Sports Management Platform',
    description: 'A Full-Stack real-time sports management system built with MEVN stack as a Progressive Web Application with secure authentication and live data synchronization.',
    tags: ['MEVN', 'Full Stack', 'PWA'],
    image: new URL('./assets/projects/Sport.png', import.meta.url).href,
    link: '#',
  },
  {
    id: 5,
    title: 'Student Information Management System',
    description: 'A comprehensive student information management system developed using HTML, CSS, and JavaScript.',
    tags: ['Frontend', 'Web Development', 'JavaScript'],
    image: new URL('./assets/projects/SIMS.png', import.meta.url).href,
    link: '#',
  },
  {
    id: 6,
    title: 'E-Commerce Electronics Store',
    description: 'An online electronics store built with a focus on user experience and seamless shopping using PHP and MySQL.',
    tags: ['PHP', 'MySQL', 'Web Development'],
    image: new URL('./assets/projects/2e622403-9a5d-437a-bf0e-d1399c3d27c6.jpg', import.meta.url).href,
    link: '#',
  },
]

const skillCategories = [
  {
    name: 'Web Development',
    skills: ['Vue.js', 'MERN Stack', 'MEVN Stack', 'React', 'TypeScript', 'Tailwind CSS', 'HTML5', 'CSS3'],
  },
  {
    name: 'Mobile & Backend',
    skills: ['Flutter', 'Node.js', 'Laravel', 'PostgreSQL', 'MongoDB', 'REST API', 'Express', 'Firebase'],
  },
  {
    name: 'Security & Tools',
    skills: ['Network Security', 'Vulnerability Assessment', 'Git', 'Canva', 'Excel', 'Database Management', 'Figma'],
  },
  {
    name: 'Leadership & Management',
    skills: ['Project Management', 'Event Coordination', 'Team Leadership', 'Public Speaking', 'Documentation', 'Organizational Skills'],
  },
]

const handleMouseMove = (e: MouseEvent) => {
  mouseX.value = e.clientX
  mouseY.value = e.clientY
}

const scrollToSection = (e: any) => {
  e.preventDefault()
  const hash = e.target.hash || e.currentTarget.hash
  if (hash) {
    const element = document.querySelector(hash)
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' })
    }
  }
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const downloadCV = () => {
  const link = document.createElement('a')
  link.href = '/src/cv/DEL ROSARIO-RESUME.pdf'
  link.download = 'DEL ROSARIO-RESUME.pdf'
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
  // Add animation classes on scroll
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
      }
    })
  }, { threshold: 0.1 })

  document.querySelectorAll('section').forEach((section) => {
    observer.observe(section)
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.portfolio {
  position: relative;
  width: 100%;
  min-height: auto;
  overflow-x: hidden;
  background: transparent;
  color: #e0e0e0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
  display: block;
}

/* Navbar */
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  height: 80px;
  background: rgba(10, 14, 39, 0.7);
  backdrop-filter: blur(20px);
  z-index: 1000;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  animation: slideDown 0.6s ease-out;
}

.navbar.navbar-scrolled {
  background: rgba(10, 14, 39, 0.95);
  height: 70px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

@keyframes slideDown {
  from {
    transform: translateY(-100%);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.nav-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 50px;
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-circle {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 18px;
  color: white;
  box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
  transition: all 0.3s ease;
  flex-shrink: 0;
}

.logo-text {
  font-size: 16px;
  font-weight: 600;
  color: #e0e0e0;
  white-space: nowrap;
  transition: all 0.3s ease;
}

.logo:hover .logo-circle {
  transform: scale(1.1) rotate(-5deg);
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.6);
}

.logo:hover .logo-text {
  color: #667eea;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 10px;
  align-items: center;
}

.nav-link {
  color: #e0e0e0;
  text-decoration: none;
  font-size: 15px;
  font-weight: 500;
  padding: 8px 16px;
  border-radius: 8px;
  position: relative;
  transition: all 0.3s ease;
}

.nav-link:hover {
  color: #667eea;
  background: rgba(102, 126, 234, 0.1);
}

.nav-cta {
  padding: 10px 28px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 20px rgba(102, 126, 234, 0.3);
}

.nav-cta:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(102, 126, 234, 0.5);
}

.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 120px 50px 60px;
  text-align: center;
  position: relative;
  width: 100%;
  background: transparent;
}

.hero-wrapper {
  width: 100%;
  max-width: 1400px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.hero-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  background: rgba(102, 126, 234, 0.1);
  border: 1px solid rgba(102, 126, 234, 0.3);
  border-radius: 25px;
  margin-bottom: 30px;
  animation: slideInDown 0.8s ease-out;
}

@keyframes slideInDown {
  from {
    transform: translateY(-20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.badge-dot {
  width: 8px;
  height: 8px;
  background: #4ade80;
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

.title {
  font-size: 80px;
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 20px;
  text-align: left;
}

.title-word {
  display: block;
  animation: fadeInUp 0.8s ease-out forwards;
}

.title-word:nth-child(1) { animation-delay: 0.1s; }
.title-word:nth-child(2) { animation-delay: 0.2s; }
.title-word:nth-child(3) { animation-delay: 0.3s; }

@keyframes fadeInUp {
  from {
    transform: translateY(30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.title-word.highlight {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.description {
  font-size: 18px;
  color: #b0b0b0;
  margin-bottom: 40px;
  line-height: 1.8;
  text-align: left;
  max-width: 600px;
  animation: fadeInUp 0.8s ease-out 0.4s backwards;
}

.hero-actions {
  display: flex;
  gap: 20px;
  animation: fadeInUp 0.8s ease-out 0.5s backwards;
}

.btn-primary, .btn-secondary {
  padding: 15px 40px;
  border: none;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 10px;
}

.btn-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(102, 126, 234, 0.6);
}

.btn-secondary {
  background: rgba(102, 126, 234, 0.1);
  color: #667eea;
  border: 2px solid rgba(102, 126, 234, 0.3);
}

.btn-secondary:hover {
  background: rgba(102, 126, 234, 0.2);
  border-color: rgba(102, 126, 234, 0.5);
  transform: translateY(-3px);
}

.arrow {
  transition: transform 0.3s ease;
}

.btn-primary:hover .arrow {
  transform: translateX(5px);
}

.hero-3d {
  height: 600px;
  animation: fadeInRight 0.8s ease-out 0.3s backwards;
  display: flex;
  align-items: flex-start;
  justify-content: center;
}

.profile-image-wrapper {
  position: relative;
  width: 80%;
  height: 80%;
  margin-top: 100px;
  padding: 12px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 24px;
  box-shadow: 0 20px 60px rgba(102, 126, 234, 0.4),
              0 0 40px rgba(102, 126, 234, 0.2),
              inset 0 0 20px rgba(255, 255, 255, 0.1);
  animation: floatImage 6s ease-in-out infinite, glowPulse 3s ease-in-out infinite;
  transition: transform 0.3s ease;
}

.profile-image-wrapper:hover {
  transform: scale(1.05);
  box-shadow: 0 25px 80px rgba(102, 126, 234, 0.6),
              0 0 60px rgba(102, 126, 234, 0.4),
              inset 0 0 30px rgba(255, 255, 255, 0.15);
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: 16px;
  display: block;
}

@keyframes floatImage {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(2deg);
  }
}

@keyframes glowPulse {
  0%, 100% {
    box-shadow: 0 20px 60px rgba(102, 126, 234, 0.4),
                0 0 40px rgba(102, 126, 234, 0.2);
  }
  50% {
    box-shadow: 0 25px 80px rgba(102, 126, 234, 0.6),
                0 0 60px rgba(102, 126, 234, 0.4);
  }
}

@keyframes fadeInRight {
  from {
    transform: translateX(100px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  animation: bobbing 3s ease-in-out infinite;
}

.scroll-dot {
  width: 8px;
  height: 8px;
  background: #667eea;
  border-radius: 50%;
  margin: 0 auto 10px;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

@keyframes bobbing {
  0%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  50% {
    transform: translateX(-50%) translateY(10px);
  }
}

.scroll-indicator p {
  font-size: 13px;
  color: #b0b0b0;
  text-transform: uppercase;
  letter-spacing: 2px;
}

/* Sections */
section {
  padding: 120px 50px;
  opacity: 0;
  transition: opacity 0.8s ease-out;
  display: block !important;
  width: 100% !important;
}

section.hero {
  opacity: 1 !important;
}

section.animate-in {
  opacity: 1;
}

.container {
  max-width: 1400px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 80px;
}

.section-title {
  font-size: 56px;
  font-weight: 900;
  margin-bottom: 20px;
  background: linear-gradient(135deg, #e0e0e0 0%, #b0b0b0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.title-underline {
  width: 80px;
  height: 4px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  margin: 20px auto 0;
  border-radius: 2px;
}

.section-subtitle {
  font-size: 18px;
  color: #b0b0b0;
  margin-top: 20px;
}

/* About Section */
.about {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.05) 0%, rgba(118, 75, 162, 0.05) 100%);
}

.about-content {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 40px;
  align-items: stretch;
}

.about-left {
  display: flex;
  flex-direction: column;
  gap: 50px;
  height: fit-content;
}

.about-card {
  padding: 50px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(102, 126, 234, 0.2);
  border-radius: 16px;
  transition: all 0.3s ease;
  margin-right: -50px;
  height: 100%;
  width: 78%;
}

.about-card:hover {
  background: rgba(102, 126, 234, 0.1);
  border-color: rgba(102, 126, 234, 0.4);
  transform: translateY(-5px);
}

.about-card h3 {
  font-size: 30px;
  margin-bottom: 20px;
  color: #667eea;
}

.about-card p {
  font-size: 20px;
  line-height: 1.8;
  color: #b0b0b0;
}

.about-image {
  display: flex;
  border-radius: 16px;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(102, 126, 234, 0.3);
  transition: all 0.3s ease;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  height: 100%;
  width: 100%;
  margin-left: -50px;
}

.about-image:hover {
  transform: translateY(-8px);
  border-color: rgba(102, 126, 234, 0.5);
  box-shadow: 0 20px 60px rgba(102, 126, 234, 0.2);
}

.about-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.3s ease;
}

.about-image:hover img {
  transform: scale(1.05);
}

/* Projects Section */
.projects {
  background: linear-gradient(135deg, rgba(118, 75, 162, 0.05) 0%, rgba(102, 126, 234, 0.05) 100%);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 40px;
}

/* Skills Section */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 50px;
}

.skill-category {
  padding: 50px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(102, 126, 234, 0.2);
  border-radius: 16px;
  transition: all 0.3s ease;
}

.skill-category:hover {
  background: rgba(102, 126, 234, 0.1);
  border-color: rgba(102, 126, 234, 0.4);
  transform: translateY(-5px);
}

.category-title {
  font-size: 22px;
  margin-bottom: 25px;
  color: #667eea;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.skill-tag {
  padding: 10px 18px;
  background: rgba(102, 126, 234, 0.15);
  border: 1px solid rgba(102, 126, 234, 0.4);
  border-radius: 20px;
  font-size: 14px;
  color: #e0e0e0;
  transition: all 0.3s ease;
  cursor: default;
}

.skill-tag:hover {
  background: rgba(102, 126, 234, 0.25);
  border-color: rgba(102, 126, 234, 0.6);
  transform: translateY(-3px);
}

/* Contact Section */
.contact {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
}

.contact-wrapper {
  text-align: center;
}

.contact-header {
  margin-bottom: 80px;
}

.contact-description {
  font-size: 18px;
  color: #b0b0b0;
  line-height: 1.8;
  max-width: 600px;
  margin: 20px auto 0;
}

.contact-links {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

.contact-link-card {
  padding: 40px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(102, 126, 234, 0.2);
  border-radius: 16px;
  text-decoration: none;
  color: inherit;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 30px;
  text-align: left;
}

.contact-link-card:hover {
  background: rgba(102, 126, 234, 0.15);
  border-color: rgba(102, 126, 234, 0.4);
  transform: translateY(-8px);
}

.link-icon {
  font-size: 48px;
  transition: transform 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  flex-shrink: 0;
}

.link-icon svg {
  width: 100%;
  height: 100%;
  color: #667eea;
  transition: color 0.3s ease;
}

.contact-link-card:hover .link-icon {
  transform: scale(1.1) rotate(10deg);
}

.link-content h4 {
  font-size: 18px;
  margin-bottom: 5px;
  color: #e0e0e0;
}

.link-content p {
  font-size: 14px;
  color: #b0b0b0;
}

.link-arrow {
  margin-left: auto;
  font-size: 24px;
  transition: transform 0.3s ease;
}

.contact-link-card:hover .link-arrow {
  transform: translateX(5px);
}

/* Footer */
.footer {
  padding: 60px 50px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(0, 0, 0, 0.2);
}

.footer-content {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-text {
  font-size: 15px;
  color: #666;
}

.heart {
  animation: heartbeat 1.5s infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.footer-links {
  display: flex;
  gap: 30px;
}

.footer-link {
  font-size: 14px;
  color: #666;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: #667eea;
}

/* Responsive */
@media (max-width: 1024px) {
  .nav-content {
    padding: 0 30px;
  }

  .hero-wrapper {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .title {
    font-size: 56px;
  }

  .hero-3d {
    height: 400px;
  }

  .section-title {
    font-size: 42px;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .navbar {
    height: 70px;
  }

  .nav-content {
    padding: 0 20px;
  }

  .nav-cta {
    display: none;
  }

  .nav-links {
    gap: 5px;
  }

  .nav-link {
    padding: 6px 12px;
    font-size: 14px;
  }

  .hero {
    padding: 100px 20px 40px;
    min-height: 80vh;
  }

  .hero-wrapper {
    grid-template-columns: 1fr;
  }

  .hero-content {
    align-items: center;
    text-align: center;
  }

  .title {
    font-size: 36px;
    text-align: center;
  }

  .description {
    text-align: center;
    margin-left: auto;
    margin-right: auto;
    font-size: 16px;
    max-width: 100%;
  }

  .hero-actions {
    justify-content: center;
    flex-direction: column;
    width: 100%;
    gap: 15px;
  }

  .btn-primary, .btn-secondary {
    width: 100%;
    padding: 14px 24px;
    font-size: 15px;
    border-radius: 10px;
  }

  .hero-3d {
    height: 300px;
    margin-top: 30px;
  }

  .profile-image-wrapper {
    width: 100%;
    margin-top: 50px;
  }

  .section-title {
    font-size: 28px;
  }

  .about-card {
    width: 100%;
    margin-right: 0;
    padding: 30px;
  }

  .about-image {
    margin-left: 0;
  }

  .about-content {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .projects-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .project-image {
    height: 150px;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }

  .contact-links {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .contact-link-card {
    flex-direction: column;
    text-align: center;
    padding: 25px;
  }

  .link-icon {
    width: 40px;
    height: 40px;
    font-size: 32px;
  }

  .link-arrow {
    margin-left: 0;
    margin-top: 10px;
  }

  section {
    padding: 60px 20px;
  }

  .section-header {
    margin-bottom: 40px;
  }

  .footer-content {
    flex-direction: column;
    gap: 20px;
  }

  .footer-links {
    gap: 20px;
  }
}

/* Extra Small Devices */
@media (max-width: 480px) {
  .navbar {
    height: 60px;
  }

  .nav-content {
    padding: 0 15px;
  }

  .logo-circle {
    width: 35px;
    height: 35px;
    font-size: 14px;
  }

  .logo-text {
    font-size: 13px;
    display: none;
  }

  .nav-link {
    padding: 6px 10px;
    font-size: 12px;
  }

  .hero {
    padding: 80px 15px 30px;
  }

  .title {
    font-size: 28px;
    line-height: 1.2;
  }

  .description {
    font-size: 14px;
    margin-bottom: 25px;
  }

  .hero-badge {
    padding: 8px 16px;
    font-size: 12px;
  }

  .hero-3d {
    height: 200px;
  }

  .section-title {
    font-size: 24px;
  }

  .section-subtitle {
    font-size: 14px;
  }

  .about-card {
    padding: 20px;
  }

  .about-card h3 {
    font-size: 22px;
  }

  .about-card p {
    font-size: 14px;
  }

  .contact-link-card {
    padding: 20px;
  }

  .link-content h4 {
    font-size: 16px;
  }

  .link-content p {
    font-size: 12px;
  }

  .skill-tag {
    font-size: 12px;
    padding: 6px 12px;
  }

  section {
    padding: 50px 15px;
  }

  .scroll-indicator {
    bottom: 20px;
  }

  .scroll-indicator p {
    font-size: 11px;
  }
}
</style>
