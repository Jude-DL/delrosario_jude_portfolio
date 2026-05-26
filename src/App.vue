<template>
  <div class="portfolio" @mousemove="handleMouseMove">
    <!-- Animated Background with Mouse Tracking -->
    <MouseTrackingBackground :mouseX="mouseX" :mouseY="mouseY" />
    
    <!-- Navigation -->
    <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
      <div class="nav-content">
        <button class="nav-toggle" @click="mobileOpen = !mobileOpen" :aria-expanded="mobileOpen" aria-label="Open navigation">☰</button>
        <div class="logo" @click="downloadCV">
          <span class="logo-text logo-white">Dev</span>
          <span class="logo-text logo-highlight">Jude</span>
          <span class="logo-text logo-white">&lt;/&gt;</span>
        </div>
        <ul class="nav-links">
          <li><a href="#home" @click="scrollToSection" class="nav-link">Home</a></li>
          <li><a href="#about" @click="scrollToSection" class="nav-link">About</a></li>
          <li><a href="#resume" @click="scrollToSection" class="nav-link">Resume</a></li>
          <li><a href="#projects" @click="scrollToSection" class="nav-link">Projects</a></li>
          <li><a href="#certification" @click="scrollToSection" class="nav-link">Certification</a></li>
          <li><a href="#skills" @click="scrollToSection" class="nav-link">Skills</a></li>
          <li><a href="#contact" @click="scrollToSection" class="nav-link">Contact</a></li>
        </ul>
        <div class="mobile-menu" v-if="mobileOpen">
          <a href="#home" @click="scrollToSection">Home</a>
          <a href="#about" @click="scrollToSection">About</a>
          <a href="#resume" @click="scrollToSection">Resume</a>
          <a href="#projects" @click="scrollToSection">Projects</a>
          <a href="#certification" @click="scrollToSection">Certification</a>
          <a href="#skills" @click="scrollToSection">Skills</a>
          <a href="#contact" @click="scrollToSection">Contact</a>
        </div>
        <div class="social-dropdown" ref="socialRef" :class="{ open: socialOpen }">
          <button class="social-btn" @click.stop="toggleSocial" aria-haspopup="true" :aria-expanded="socialOpen">
            <span class="social-label">Social</span>
            <span class="caret" aria-hidden="true">▾</span>
          </button>
          <div v-if="socialOpen" class="dropdown-menu" role="menu">
            <a class="dropdown-item" href="https://www.facebook.com/jude.delrosario.52/" target="_blank" rel="noopener noreferrer">
              <span class="item-icon" aria-hidden="true">
                <img :src="fbIcon" alt="Facebook" />
              </span>
              <span>Facebook</span>
            </a>
            <a class="dropdown-item" href="https://github.com/Jude-DL" target="_blank" rel="noopener noreferrer">
              <span class="item-icon" aria-hidden="true">
                <img :src="ghIcon" alt="GitHub" />
              </span>
              <span>GitHub</span>
            </a>
            <a class="dropdown-item" href="https://ph.jobstreet.com/profiles/judechristian-delrosario-pN77rgfYXQ" target="_blank" rel="noopener noreferrer">
              <span class="item-icon" aria-hidden="true">
                <img :src="jsIcon" alt="JobStreet" />
              </span>
              <span>JobStreet</span>
            </a>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="hero-wrapper">
        <div class="hero-content">
          <h1 class="title">
            <span class="title-word">JUDE</span>
            <span class="title-word">CHRISTIAN</span>
            <span class="title-word highlight">DEL ROSARIO</span>
          </h1>
          <p class="description">Information Technology student and aspiring software developer.</p>
          <div class="hero-actions">
            <button class="btn-primary" @click="downloadCV">
              Download CV
            </button>
            <button class="btn-secondary" @click="scrollToHash('#contact')">
              Get In Touch
            </button>
          </div>
        </div>
        <div class="hero-3d">
          <div class="profile-image-wrapper">
            <img :src="profileImage" alt="Jude Christian Del Rosario" class="profile-image" />

            <div class="profile-chat" role="status" aria-live="polite">
              <div class="chat-bubble">
                <span class="typing-dots" aria-hidden="true">
                  <i></i><i></i><i></i>
                </span>
                <span class="typing-text">Hi, I'm Jude!</span>
              </div>
            </div>
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
              <p>I'm Jude Christian D. Del Rosario, a Bachelor of Science in Information Technology student at the University of Cabuyao, expected to graduate in June 2026. I build my work around full-stack development, database management, network security, and practical leadership.</p>
            </div>
            <div class="about-card">
              <h3>What I Do</h3>
              <p>I develop mobile and web applications with Flutter, Vue.js, Laravel, Firebase, React, and the MERN/MEVN stacks. I also bring experience in network monitoring, project coordination, event management, research, and student leadership roles that strengthen team execution.</p>
            </div>
          </div>
          <div class="about-image">
            <img :src="awardImage" alt="Jude Christian Del Rosario presenting his profile" />
          </div>
        </div>
      </div>
    </section>

    <!-- Resume Navigator Section -->
    <section id="resume" class="resume">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Interactive Resume</h2>
          <div class="title-underline"></div>
          <p class="section-subtitle">Explore my background like a guided portfolio</p>
        </div>

        <div class="resume-shell">
          <div class="resume-tabs" role="tablist" aria-label="Resume sections">
            <button
              v-for="page in resumePages"
              :key="page.key"
              class="resume-tab"
              :class="{ active: activeResumePage === page.key }"
              type="button"
              @click="activeResumePage = page.key"
            >
              <span class="resume-tab-index">0{{ page.index }}</span>
              <span>{{ page.label }}</span>
            </button>
          </div>

          <div class="resume-panel">
            <div class="resume-panel-head">
              <div>
                <p class="resume-kicker">{{ activeResumePageData.kicker }}</p>
                <h3>{{ activeResumePageData.title }}</h3>
              </div>
              <button class="btn-secondary btn-mini" type="button" @click="scrollToHash('#contact')">
                Hire Me
              </button>
            </div>

            <p class="resume-summary">{{ activeResumePageData.summary }}</p>

            <div v-if="activeResumePage === 'summary'" class="resume-story-grid">
              <div class="resume-story-card">
                <span class="story-label">Focus</span>
                <p>Full-stack development, network security, mobile apps, and solution-oriented leadership.</p>
              </div>
              <div class="resume-story-card">
                <span class="story-label">Approach</span>
                <p>I build systems that are practical, polished, and easy for real users to adopt.</p>
              </div>
              <div class="resume-story-card">
                <span class="story-label">Style</span>
                <p>Clean interfaces, interactive motion, and reliable deployment workflows.</p>
              </div>
            </div>

            <div v-else-if="activeResumePage === 'experience'" class="timeline-list">
              <article v-for="item in experienceItems" :key="item.title" class="timeline-card">
                <div class="timeline-top">
                  <div>
                    <h4>{{ item.title }}</h4>
                    <p>{{ item.org }} | {{ item.period }}</p>
                  </div>
                  <span class="timeline-pill">{{ item.role }}</span>
                </div>
                <ul>
                  <li v-for="point in item.points" :key="point">{{ point }}</li>
                </ul>
              </article>
            </div>

            <div v-else-if="activeResumePage === 'projects'" class="spotlight-grid">
              <article v-for="project in featuredProjects" :key="project.id" class="spotlight-card">
                <img :src="project.image" :alt="project.title" />
                <div>
                  <h4>{{ project.title }}</h4>
                  <p>{{ project.description }}</p>
                  <div class="spotlight-tags">
                    <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                  </div>
                </div>
              </article>
            </div>

            <div v-else-if="activeResumePage === 'education'" class="education-grid">
              <div class="education-card">
                <p class="resume-kicker">Education</p>
                <h4>University of Cabuyao</h4>
                <p>Bachelor of Science in Information Technology</p>
                <span>2022 - Present | Expected Graduation: June 10, 2026</span>
              </div>
              <div class="education-card">
                <p class="resume-kicker">Research</p>
                <h4>Competitive Research Experience</h4>
                <p>Principal researcher in regional and university research competitions.</p>
                <span>Presentation, analysis, and technical communication</span>
              </div>
            </div>

            <div v-else class="badge-grid">
              <div v-for="badge in credentialHighlights" :key="badge.title" class="badge-card">
                <span class="badge-type">{{ badge.type }}</span>
                <h4>{{ badge.title }}</h4>
                <p>{{ badge.detail }}</p>
              </div>
            </div>
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

    <!-- Certifications Section -->
    <section id="certification" class="certification">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Certifications & Awards</h2>
          <div class="title-underline"></div>
          <p class="section-subtitle">Selected credentials that support my technical and leadership growth</p>
        </div>

        <div class="cert-carousel">
          <div class="cert-preview">
            <img
              :src="activeCertificate.image"
              :alt="activeCertificate.title"
              class="cert-image"
            />
            <button
              type="button"
              class="cert-nav cert-nav-prev"
              @click="prevCertificate"
              aria-label="Previous certificate"
            >
              ‹
            </button>
            <button
              type="button"
              class="cert-nav cert-nav-next"
              @click="nextCertificate"
              aria-label="Next certificate"
            >
              ›
            </button>
          </div>

          <div class="cert-details-card">
            <span class="cert-meta">{{ activeCertificate.year }}</span>
            <h3>{{ activeCertificate.title }}</h3>
            <p class="cert-issuer">{{ activeCertificate.issuer }}</p>
            <p class="cert-context">{{ activeCertificate.context }}</p>
            <div class="cert-counter">
              {{ activeCertificateIndex + 1 }} / {{ certifications.length }}
            </div>
          </div>

          <div class="cert-thumbnails" role="tablist" aria-label="Certificate previews">
            <button
              v-for="(cert, index) in certifications"
              :key="cert.title"
              type="button"
              class="cert-thumb"
              :class="{ active: activeCertificateIndex === index }"
              @click="setActiveCertificate(index)"
              :aria-label="`View ${cert.title}`"
            >
              <img :src="cert.image" :alt="cert.title" />
            </button>
          </div>
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
              <span class="skill-tag" v-for="skill in category.skills" :key="skill.name">
                <img :src="skill.icon" :alt="skill.name" class="skill-icon" loading="lazy" />
                {{ skill.name }}
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

    <button
      type="button"
      class="lemi-toggle"
      @click="toggleLemi"
      :aria-expanded="lemiOpen"
      aria-controls="lemi-chat-panel"
    >
      <span class="lemi-toggle-icon" aria-hidden="true">{{ lemiOpen ? '×' : '✦' }}</span>
      <span class="lemi-toggle-label">Lemi AI</span>
    </button>

    <aside
      v-if="lemiOpen"
      id="lemi-chat-panel"
      class="lemi-chat"
      role="dialog"
      aria-label="Lemi AI chat assistant"
    >
      <header class="lemi-header">
        <div>
          <p class="lemi-kicker">Your Portfolio Assistant</p>
          <h3>Lemi AI</h3>
        </div>
        <button type="button" class="lemi-close" @click="lemiOpen = false" aria-label="Close Lemi AI">×</button>
      </header>

      <div class="lemi-messages" ref="lemiMessagesRef">
        <article
          v-for="message in lemiMessages"
          :key="message.id"
          class="lemi-message"
          :class="message.role"
        >
          <p>{{ message.text }}</p>
        </article>

        <article v-if="lemiTyping" class="lemi-message assistant lemi-typing">
          <p>Lemi AI is typing...</p>
        </article>
      </div>

      <div class="lemi-quick-asks">
        <button
          v-for="prompt in lemiQuickPrompts"
          :key="prompt"
          type="button"
          class="lemi-quick-btn"
          @click="askLemiQuickPrompt(prompt)"
        >
          {{ prompt }}
        </button>
      </div>

      <form class="lemi-form" @submit.prevent="sendLemiMessage">
        <input
          v-model="lemiInput"
          type="text"
          class="lemi-input"
          placeholder="Ask anything about Jude..."
          maxlength="220"
        />
        <button type="submit" class="lemi-send" :disabled="!lemiInput.trim() || lemiTyping">Send</button>
      </form>
    </aside>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'
import MouseTrackingBackground from './components/MouseTrackingBackground.vue'
import ProjectCard from './components/ProjectCard.vue'
import awardImage from './assets/IMG_7603.jpg'
import profileImage from './assets/25f9482b-da02-469d-be6d-51891a4fc50e.png'
import fbIcon from './assets/icons/facebook.svg'
import ghIcon from './assets/icons/github.svg'
import jsIcon from './assets/icons/jobstreet.svg'

const mouseX = ref(0)
const mouseY = ref(0)
const isScrolled = ref(false)
const socialOpen = ref(false)
const mobileOpen = ref(false)
const socialRef = ref<HTMLElement | null>(null)
const activeResumePage = ref<'summary' | 'experience' | 'projects' | 'education' | 'credentials'>('summary')

const resumePages = [
  { key: 'summary', label: 'Summary', index: 1 },
  { key: 'experience', label: 'Experience', index: 2 },
  { key: 'projects', label: 'Projects', index: 3 },
  { key: 'education', label: 'Education', index: 4 },
  { key: 'credentials', label: 'Credentials', index: 5 },
] as const

const resumePageDetails = {
  summary: {
    kicker: 'Profile Snapshot',
    title: 'Technical foundation with leadership depth',
    summary: 'Information Technology student with a strong foundation in full-stack development, database management, and network security. I combine technical proficiency with strategic planning and team leadership.',
  },
  experience: {
    kicker: 'Career Experience',
    title: 'Roles that shaped my execution style',
    summary: 'Hands-on experience across networking, student governance, event operations, and organizational leadership.'
  },
  projects: {
    kicker: 'Selected Work',
    title: 'Real products with practical outcomes',
    summary: 'A mix of mobile, web, and systems projects built with Flutter, Vue, Laravel, Firebase, and deployment tooling.'
  },
  education: {
    kicker: 'Academic Path',
    title: 'Learning built around applied computing',
    summary: 'Formal study in information technology, paired with research and competition experience that sharpened technical communication.'
  },
  credentials: {
    kicker: 'Proof Points',
    title: 'Certifications and awards that reinforce the profile',
    summary: 'Cybersecurity, data, networking, and recognition milestones that support my technical and professional growth.'
  },
} as const

const activeResumePageData = computed(() => resumePageDetails[activeResumePage.value])

const toggleSocial = () => {
  socialOpen.value = !socialOpen.value
}

const featuredProjects = computed(() => projects.slice(0, 3))

const projects = [
  {
    id: 1,
    title: 'POLICE-NOW',
    description: 'A mobile based real time emergency response and police assistance application.',
    tags: ['Full Stack', 'Web Development', 'Mobile Development'],
    image: new URL('./assets/projects/Black and White Minimalist Elegant Modern Typography  Creative Studio Brand Logo.png', import.meta.url).href,
    link: 'https://police-now-landingpage-n37m.vercel.app/',
  },
  {
    id: 2,
    title: 'CCS Intensive Profiling System',
    description: 'Multi-role web-based profiling system built with Vue.js and Laravel to manage student, faculty, and administrative workflows. Features onboarding surveys, personalized recommendations, QR-based event ticketing, role-specific dashboards, and secure data handling.',
    tags: ['Full Stack', 'Vue.js', 'Laravel'],
    image: new URL('./assets/projects/CCS Portal.png', import.meta.url).href,
    link: 'https://ccs-intensive-profiling-system-rkcr.vercel.app/',
  },
  {
    id: 3,
    title: 'Task Management System',
    description: 'A full-stack task management system using Laravel and React. Includes user authentication, task assignment, and progress tracking features.',
    tags: ['Laravel', 'React', 'Full Stack'],
    image: new URL('./assets/projects/Task.png', import.meta.url).href,
    link: '#',
    deployed: false,
  },
  {
    id: 4,
    title: 'MEVN Sports Management Platform',
    description: 'A Full-Stack real-time sports management system built with MEVN stack as a Progressive Web Application with secure authentication and live data synchronization.',
    tags: ['MEVN', 'Full Stack', 'PWA'],
    image: new URL('./assets/projects/Sport.png', import.meta.url).href,
    link: '#',
    deployed: false,
  },
  {
    id: 5,
    title: 'MERN User Management System',
    description: 'Full-stack web application built with MongoDB, Express, React, and Node.js. Features real-time data synchronization and responsive design.',
    tags: ['MERN', 'Full Stack', 'JavaScript'],
    image: new URL('./assets/projects/Mern.png', import.meta.url).href,
    link: '#',
    deployed: false,
  },
  {
    id: 6,
    title: 'E-Commerce Electronics Store',
    description: 'An online electronics store built with a focus on user experience and seamless shopping using PHP and MySQL.',
    tags: ['PHP', 'MySQL', 'Web Development'],
    image: new URL('./assets/projects/2e622403-9a5d-437a-bf0e-d1399c3d27c6.jpg', import.meta.url).href,
    link: '#',
    deployed: false,
  },
]

const skillCategories = [
  {
    name: 'Web Development',
    skills: [
      { name: 'Vue.js', icon: 'https://cdn.simpleicons.org/vuedotjs' },
      { name: 'MERN Stack', icon: 'https://cdn.simpleicons.org/mongodb' },
      { name: 'MEVN Stack', icon: 'https://cdn.simpleicons.org/vuedotjs' },
      { name: 'React', icon: 'https://cdn.simpleicons.org/react' },
      { name: 'TypeScript', icon: 'https://cdn.simpleicons.org/typescript' },
      { name: 'Tailwind CSS', icon: 'https://cdn.simpleicons.org/tailwindcss' },
      { name: 'HTML5', icon: 'https://cdn.simpleicons.org/html5' },
      { name: 'CSS3', icon: 'https://cdn.simpleicons.org/css' },
    ],
  },
  {
    name: 'Mobile & Backend',
    skills: [
      { name: 'Flutter', icon: 'https://cdn.simpleicons.org/flutter' },
      { name: 'Node.js', icon: 'https://cdn.simpleicons.org/nodedotjs' },
      { name: 'Laravel', icon: 'https://cdn.simpleicons.org/laravel' },
      { name: 'PostgreSQL', icon: 'https://cdn.simpleicons.org/postgresql' },
      { name: 'MongoDB', icon: 'https://cdn.simpleicons.org/mongodb' },
      { name: 'REST API', icon: 'https://cdn.simpleicons.org/postman' },
      { name: 'Express', icon: 'https://cdn.simpleicons.org/express' },
      { name: 'Firebase', icon: 'https://cdn.simpleicons.org/firebase' },
    ],
  },
  {
    name: 'Security & Tools',
    skills: [
      { name: 'Network Security', icon: 'https://cdn.simpleicons.org/cisco' },
      { name: 'Vulnerability Assessment', icon: 'https://cdn.simpleicons.org/owasp' },
      { name: 'Git', icon: 'https://cdn.simpleicons.org/git' },
      { name: 'Canva', icon: 'https://cdn.simpleicons.org/canva' },
      { name: 'Excel', icon: 'https://cdn.simpleicons.org/microsoftexcel' },
      { name: 'Database Management', icon: 'https://cdn.simpleicons.org/mysql' },
      { name: 'Figma', icon: 'https://cdn.simpleicons.org/figma' },
    ],
  },
  {
    name: 'Leadership & Management',
    skills: [
      { name: 'Project Management', icon: 'https://cdn.simpleicons.org/jira' },
      { name: 'Event Coordination', icon: 'https://cdn.simpleicons.org/googlecalendar' },
      { name: 'Team Leadership', icon: 'https://cdn.simpleicons.org/microsoftteams' },
      { name: 'Public Speaking', icon: 'https://cdn.simpleicons.org/googleslides' },
      { name: 'Documentation', icon: 'https://cdn.simpleicons.org/notion' },
      { name: 'Organizational Skills', icon: 'https://cdn.simpleicons.org/clickup' },
    ],
  },
]

const experienceItems = [
  {
    title: 'Royal CableVision',
    org: 'Network Monitoring/Engineer Intern',
    period: '2026',
    role: 'Internship',
    points: [
      'Assisted in monitoring network traffic and implemented security protocols to improve reliability.',
      'Collaborated with technical teams to troubleshoot issues and improve operational efficiency by 20%.',
      'Documented network configurations and maintenance routines for continuity and knowledge transfer.',
    ],
  },
  {
    title: 'CCS Student Government',
    org: '4th Year Representative',
    period: '2025 - 2026',
    role: 'Leadership',
    points: [
      'Liaised between students and administration to advocate for campus needs and concerns.',
      'Organized engagement initiatives that contributed to a 15% increase in participation.',
    ],
  },
  {
    title: 'SITeS Organization',
    org: 'Internal Vice President',
    period: '2023 - 2025',
    role: 'Operations',
    points: [
      'Oversaw organizational operations and strategic initiatives.',
      'Improved member engagement through feedback sessions and regular collaboration.',
    ],
  },
]

const certifications = [
  {
    title: 'Introduction to SQL',
    issuer: 'DataCamp',
    year: '2026',
    context: 'Statement of accomplishment for completing SQL fundamentals.',
    image: new URL('./assets/certs/Introduction to SQL.png', import.meta.url).href,
  },
  {
    title: 'Junior Cybersecurity Analyst Career Path Exam',
    issuer: 'Cisco Networking Academy',
    year: '2026',
    context: 'Career path exam certificate under DICT-CISCO track.',
    image: new URL('./assets/certs/Junior_Cybersecurity_Analyst_Career_Path_Exam.png', import.meta.url).href,
  },
  {
    title: 'Ethical Hacker',
    issuer: 'Cisco Networking Academy',
    year: '2026',
    context: 'Completion certificate in ethical hacking concepts and practices.',
    image: new URL('./assets/certs/Ethical_Hacker.png', import.meta.url).href,
  },
  {
    title: 'Data Science Essentials with Python',
    issuer: 'Cisco Networking Academy',
    year: '2026',
    context: 'Data science foundations and Python data workflow completion.',
    image: new URL('./assets/certs/Data_Science_Essentials_with_Python.png', import.meta.url).href,
  },
  {
    title: 'Introduction to Cybersecurity',
    issuer: 'Cisco Networking Academy',
    year: '2026',
    context: 'Foundational cybersecurity concepts and threat awareness.',
    image: new URL('./assets/certs/Introduction_to_Cybersecurity.png', import.meta.url).href,
  },
  {
    title: 'Networking Basics',
    issuer: 'DICT-ITU DTC Initiative / Cisco Networking Academy',
    year: '2026',
    context: 'Networking fundamentals and infrastructure basics.',
    image: new URL('./assets/certs/Networking_Basics.png', import.meta.url).href,
  },
  {
    title: 'Research Presentation Finalist',
    issuer: 'University of Cabuyao',
    year: '2026',
    context: 'Certificate of research presentation as finalist.',
    image: new URL('./assets/certs/Certificate of Research Presentation as Finalist.jpg', import.meta.url).href,
  },
  {
    title: '2nd Place - STCIEERD Undergraduate R&D Competition',
    issuer: 'STCIEERD / Batangas State University',
    year: '2025',
    context: 'Recognition for winning 2nd place in research and development competition.',
    image: new URL('./assets/certs/Recognition in the 1st STCIEERD Undergraduate Research and Development Competition,.png', import.meta.url).href,
  },
  {
    title: 'Research Paper Presentation - STCIEERD Competition',
    issuer: 'STCIEERD / Batangas State University',
    year: '2025',
    context: 'Certificate of recognition for presenting Police-Now research paper.',
    image: new URL('./assets/certs/in the 1st STCIEERD Undergraduate Research and Development Competition,.png', import.meta.url).href,
  },
  {
    title: 'NSTP Exemplary Awardee',
    issuer: 'University of Cabuyao',
    year: '2023',
    context: 'Recognition as exemplary awardee in NSTP CWTS.',
    image: new URL('./assets/certs/NSTP Exemplary Awardee.png', import.meta.url).href,
  },
  {
    title: 'Warehouse Safety and Security 101',
    issuer: 'Lazada / Logicore Inc.',
    year: '2021',
    context: 'Certificate of attendance for annual safety and security awareness training.',
    image: new URL('./assets/certs/Warehouse Safety and Security 101-Best Practices Guidelines..png', import.meta.url).href,
  },
]

const activeCertificateIndex = ref(0)
const activeCertificate = computed<(typeof certifications)[number]>(
  () => certifications[activeCertificateIndex.value] ?? certifications[0]!
)

const setActiveCertificate = (index: number) => {
  activeCertificateIndex.value = index
}

const nextCertificate = () => {
  activeCertificateIndex.value = (activeCertificateIndex.value + 1) % certifications.length
}

const prevCertificate = () => {
  activeCertificateIndex.value = (activeCertificateIndex.value - 1 + certifications.length) % certifications.length
}

type LemiMessage = {
  id: number
  role: 'assistant' | 'user'
  text: string
}

const lemiOpen = ref(false)
const lemiInput = ref('')
const lemiTyping = ref(false)
const lemiMessagesRef = ref<HTMLElement | null>(null)
const lemiMessageId = ref(1)
const lemiQuickPrompts = [
  'What are your top projects?',
  'What skills do you use?',
  'How can I contact you?',
  'Tell me about your certifications',
]

const lemiMessages = ref<LemiMessage[]>([
  {
    id: lemiMessageId.value++,
    role: 'assistant',
    text: "Hi! I’m Lemi AI 👋 Ask me anything about Jude’s background, projects, skills, certifications, or how to contact him.",
  },
])

const scrollLemiToBottom = () => {
  requestAnimationFrame(() => {
    if (lemiMessagesRef.value) {
      lemiMessagesRef.value.scrollTop = lemiMessagesRef.value.scrollHeight
    }
  })
}

const buildLemiReply = (question: string) => {
  const query = question.toLowerCase()

  if (query.includes('name') || query.includes('who are you') || query.includes('who is')) {
    return 'His name is Jude Christian D. Del Rosario, an Information Technology student at the University of Cabuyao.'
  }

  if (query.includes('about') || query.includes('background') || query.includes('introduce')) {
    return 'Jude focuses on full-stack development, mobile apps, database systems, and network security, while also leading teams and student initiatives.'
  }

  if (query.includes('graduate') || query.includes('education') || query.includes('school') || query.includes('university')) {
    return 'He is taking BS Information Technology at the University of Cabuyao and is expected to graduate on June 10, 2026.'
  }

  if (query.includes('experience') || query.includes('intern') || query.includes('leadership')) {
    return 'He has internship experience in network monitoring at Royal CableVision and leadership roles in CCS Student Government and SITeS Organization.'
  }

  if (query.includes('project') || query.includes('portfolio') || query.includes('built')) {
    const projectNames = projects.slice(0, 4).map((project) => project.title).join(', ')
    return `His featured projects include ${projectNames}. You can open the Projects section for full details and technology stacks.`
  }

  if (query.includes('skill') || query.includes('technology') || query.includes('tech stack')) {
    const highlightedSkills = skillCategories
      .flatMap((category) => category.skills.map((skill) => skill.name))
      .slice(0, 10)
      .join(', ')
    return `His core skills include ${highlightedSkills}, plus strong capability in leadership, documentation, and project execution.`
  }

  if (query.includes('certification') || query.includes('certificate') || query.includes('award')) {
    const certHighlights = certifications
      .slice(0, 3)
      .map((cert) => cert.title)
      .join(', ')
    return `Notable credentials include ${certHighlights}, along with multiple research and academic recognitions.`
  }

  if (query.includes('contact') || query.includes('email') || query.includes('hire') || query.includes('reach')) {
    return 'You can contact Jude at delrosariojude61@gmail.com, or connect through LinkedIn and GitHub in the Contact section.'
  }

  if (query.includes('cv') || query.includes('resume')) {
    return 'You can download his CV from the hero section using the “Download CV” button, and explore the interactive resume section for a guided overview.'
  }

  return 'I can help with Jude’s background, projects, skills, certifications, resume, and contact details. Try asking: “What are his top projects?”'
}

const sendLemiMessage = async () => {
  const text = lemiInput.value.trim()
  if (!text || lemiTyping.value) return

  lemiMessages.value.push({
    id: lemiMessageId.value++,
    role: 'user',
    text,
  })

  lemiInput.value = ''
  lemiTyping.value = true
  scrollLemiToBottom()

  const response = buildLemiReply(text)
  await new Promise((resolve) => setTimeout(resolve, 500))

  lemiMessages.value.push({
    id: lemiMessageId.value++,
    role: 'assistant',
    text: response,
  })

  lemiTyping.value = false
  scrollLemiToBottom()
}

const askLemiQuickPrompt = (prompt: string) => {
  if (lemiTyping.value) return
  lemiInput.value = prompt
  sendLemiMessage()
}

const toggleLemi = () => {
  lemiOpen.value = !lemiOpen.value
  if (lemiOpen.value) {
    scrollLemiToBottom()
  }
}

const credentialHighlights = [
  { type: 'Certification', title: 'Cybersecurity & Data', detail: 'DICT-CISCO cybersecurity, ethical hacking, Python data science, and SQL.' },
  { type: 'Award', title: 'Academic Recognition', detail: 'Dean\'s Lister, Service Awardee, and capstone recognition.' },
  { type: 'Award', title: 'Research Results', detail: 'Finalist and placer recognition from regional and university competitions.' },
]

const handleMouseMove = (e: MouseEvent) => {
  mouseX.value = e.clientX
  mouseY.value = e.clientY
}

const scrollToSection = (event: MouseEvent) => {
  event.preventDefault()
  const hash = (event.currentTarget as HTMLAnchorElement | null)?.hash
    || (event.target as HTMLElement | null)?.closest('a')?.getAttribute('href')

  if (hash) {
    const element = document.querySelector(hash)
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' })
    }
  }
  // close mobile menu when a nav link is tapped
  mobileOpen.value = false
}

const scrollToHash = (hash: string) => {
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
  link.href = '/src/cv/JUDE DEL ROSARIO_CV.pdf'
  link.download = 'JUDE DEL ROSARIO_CV.pdf'
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  document.addEventListener('click', handleClickOutside)
  
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
  document.removeEventListener('click', handleClickOutside)
})

const handleClickOutside = (e: MouseEvent) => {
  if (socialRef.value && !socialRef.value.contains(e.target as Node)) {
    socialOpen.value = false
  }
}
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
  justify-content: center;
  align-items: center;
  position: relative;
}

.logo {
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 12px;
  position: absolute;
  left: 50px;
}

.logo-img {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  object-fit: cover;
  box-shadow: 0 5px 20px rgba(0,0,0,0.25);
  flex-shrink: 0;
}

.logo-text {
  font-size: 16px;
  font-weight: 800;
  color: #ffffff;
  white-space: nowrap;
  transition: all 0.3s ease;
}

.logo-highlight {
  color: var(--primary-1);
}

.logo-white {
  color: #ffffff;
}

.logo:hover .logo-circle {
  transform: scale(1.1) rotate(-5deg);
  box-shadow: 0 10px 30px var(--primary-glow);
}

.logo:hover .logo-text {
  opacity: 0.92;
}

.logo:hover .logo-highlight {
  color: var(--primary-2);
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 18px;
  align-items: center;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

.nav-toggle {
  display: none;
  position: absolute;
  right: 50px;
  top: 50%;
  transform: translateY(-50%);
  background: transparent;
  border: none;
  color: #e0e0e0;
  font-size: 22px;
  padding: 8px;
  cursor: pointer;
  z-index: 1300;
}

.mobile-menu {
  display: none;
}

.social-dropdown {
  position: absolute;
  right: 50px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1200;
}

.social-btn {
  height: 44px;
  padding: 0 14px;
  border-radius: 12px;
  background: rgba(255,255,255,0.03);
  color: #e0e0e0;
  border: 1px solid rgba(255,255,255,0.04);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.18s ease;
  font-weight: 600;
  font-size: 14px;
}

.social-btn:hover {
  transform: translateY(-2px);
  background: rgba(102,126,234,0.08);
}

.social-label {
  display: inline-block;
  line-height: 1;
}

.dropdown-menu {
  position: absolute;
  top: calc(100% + 8px);
  right: 0;
  min-width: 210px;
  background: rgba(0,0,0,0.85);
  border-radius: 10px;
  padding: 8px;
  box-shadow: 0 12px 40px rgba(0,0,0,0.6);
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.dropdown-item {
  display: flex;
  gap: 10px;
  align-items: center;
  padding: 10px 12px;
  color: #e0e0e0;
  text-decoration: none;
  border-radius: 8px;
  transition: background 0.15s ease;
}

.dropdown-item:hover {
  background: rgba(102,126,234,0.06);
}

.item-icon {
  width: 32px;
  height: 32px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  background: rgba(0,0,0,0.55);
  font-size: 14px;
  font-weight: 700;
  color: #ffffff;
}

.dropdown-item svg {
  width: 18px;
  height: 18px;
  color: white;
  fill: currentColor;
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
  color: var(--primary-1);
  background: rgba(255,122,26,0.08);
}

.nav-cta {
  padding: 10px 28px;
  background: linear-gradient(135deg, var(--primary-1) 0%, var(--primary-2) 100%);
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 20px var(--primary-glow);
}
.social-dropdown .caret {
  display: inline-block;
  margin-left: 8px;
  transition: transform 0.18s ease;
  font-size: 12px;
}

.social-dropdown.open .caret {
  transform: rotate(180deg);
}

.nav-cta:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px var(--primary-glow);
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
  margin-left: 40px;
  transition: margin 0.25s ease;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  background: rgba(255, 122, 26, 0.08);
  border: 1px solid rgba(255, 122, 26, 0.22);
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
  background: linear-gradient(135deg, var(--primary-1) 0%, var(--primary-2) 100%);
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
  background: linear-gradient(135deg, var(--primary-1) 0%, var(--primary-2) 100%);
  color: white;
  box-shadow: 0 10px 30px var(--primary-glow);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px var(--primary-glow);
}

.btn-secondary {
  background: rgba(255,122,26,0.06);
  color: var(--primary-1);
  border: 2px solid rgba(255,122,26,0.22);
}

.btn-secondary:hover {
  background: rgba(255,122,26,0.16);
  border-color: rgba(255,122,26,0.32);
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
  border-radius: 24px;
  box-shadow: 0 20px 60px var(--primary-glow),
              0 0 40px rgba(255,122,26,0.12),
              inset 0 0 20px rgba(255, 255, 255, 0.1);
  animation: floatImage 6s ease-in-out infinite, glowPulse 3s ease-in-out infinite;
  margin-left: 40px;
  overflow: visible;
  transition: margin 0.25s ease, transform 0.3s ease;
}

.profile-image-wrapper:hover {
  transform: scale(1.05);
  box-shadow: 0 25px 80px var(--primary-glow),
              0 0 60px rgba(255,122,26,0.35),
              inset 0 0 30px rgba(255, 255, 255, 0.15);
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: 16px;
  display: block;
}

/* Small speech bubble overlay with typing animation */
.profile-chat {
  position: absolute;
  top: 14px;
  right: 14px;
  left: auto;
  z-index: 30;
  pointer-events: none;
}


.chat-bubble {
  position: relative;
  background: linear-gradient(180deg, rgba(14,14,14,0.9), rgba(6,6,6,0.88));
  color: #fff;
  padding: 10px 14px;
  border-radius: 14px;
  border: 1px solid var(--glass-border);
  box-shadow: 0 10px 30px var(--primary-glow);
  font-weight: 700;
  font-size: 14px;
  line-height: 1;
  max-width: 20ch;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  white-space: nowrap;
  transform-origin: bottom left;
  animation: bubbleIn 420ms cubic-bezier(.2,.9,.2,1) both;
}

/* tail */
.chat-bubble::after {
  content: '';
  position: absolute;
  left: 18px;
  right: auto;
  bottom: -6px;
  width: 14px;
  height: 14px;
  background: inherit;
  transform: rotate(45deg);
  border-left: 1px solid rgba(255,120,40,0.08);
}

/* thought-dot chain to the left of the bubble */
.profile-chat::before {
  content: '';
  position: absolute;
  left: -10px;
  bottom: 6px;
  width: 8px;
  height: 8px;
  background: rgba(255,255,255,0.06);
  border-radius: 50%;
  box-shadow: 14px 6px 0 rgba(255,255,255,0.04), 28px 12px 0 rgba(255,255,255,0.02);
  transform: translateX(-6px);
}

/* Keep bubble text clean and stable on load. */
.typing-dots { display: none; }
.typing-dots i { width: 6px; height: 6px; background: rgba(255,255,255,0.18); border-radius: 50%; display: inline-block; transform: translateY(0); }
.typing-dots i:nth-child(1) { animation: dotBounce 1s infinite 0s; }
.typing-dots i:nth-child(2) { animation: dotBounce 1s infinite 0.15s; }
.typing-dots i:nth-child(3) { animation: dotBounce 1s infinite 0.3s; }

@keyframes dotBounce {
  0%, 80%, 100% { transform: translateY(0); opacity: 0.6; }
  40% { transform: translateY(-6px); opacity: 1; }
}

/* typewriter text appears after dots */
.typing-text {
  display: inline-block;
  white-space: nowrap;
  overflow: visible;
  width: auto;
  color: var(--primary-1);
  border-right: none;
  opacity: 1;
  animation: none;
}

@keyframes textReveal {
  from { width: 0ch; }
  to { width: 12ch; }
}

@keyframes textFade { to { opacity: 1; } }

@keyframes bubbleIn {
  from { transform: translateY(8px) scale(.96); opacity: 0; }
  to { transform: translateY(0) scale(1); opacity: 1; }
}

@media (max-width: 768px) {
  .profile-chat {
    top: 8px;
    left: 0;
    right: 0;
    transform: none;
    display: flex;
    justify-content: center;
    padding: 0 10px;
  }

  .chat-bubble {
    font-size: 12px;
    padding: 8px 10px;
    width: fit-content;
    max-width: 100%;
  }
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
    box-shadow: 0 20px 60px var(--primary-glow),
                0 0 40px rgba(255,122,26,0.12);
  }
  50% {
    box-shadow: 0 25px 80px rgba(255,122,26,0.45),
                0 0 60px rgba(255,122,26,0.28);
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
  background: var(--primary-1);
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
  background: linear-gradient(135deg, var(--primary-1) 0%, var(--primary-2) 100%);
  margin: 20px auto 0;
  border-radius: 2px;
}

.section-subtitle {
  font-size: 18px;
  color: #b0b0b0;
  margin-top: 20px;
}

/* Resume Section */
.resume {
  background: linear-gradient(135deg, rgba(255,255,255,0.02) 0%, rgba(30,18,12,0.06) 100%);
}

.resume-shell {
  display: grid;
  grid-template-columns: 280px 1fr;
  gap: 30px;
  align-items: start;
}

.resume-tabs {
  display: flex;
  flex-direction: column;
  gap: 14px;
  position: sticky;
  top: 110px;
}

.resume-tab {
  border: 1px solid rgba(255,122,26,0.12);
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.04);
  color: #e0e0e0;
  padding: 18px 20px;
  text-align: left;
  display: flex;
  align-items: center;
  gap: 14px;
  cursor: pointer;
  transition: all 0.25s ease;
}

.resume-tab:hover,
.resume-tab.active {
  background: linear-gradient(135deg, rgba(255,122,26,0.18), rgba(255,77,0,0.14));
  border-color: rgba(255,122,26,0.32);
  transform: translateX(6px);
}

.resume-tab-index {
  width: 34px;
  height: 34px;
  border-radius: 10px;
  background: rgba(255,122,26,0.18);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: 700;
  color: #fff6ec;
  flex-shrink: 0;
}

.resume-panel {
  padding: 34px;
  border-radius: 28px;
  background: rgba(12, 8, 6, 0.76);
  border: 1px solid rgba(255,122,26,0.12);
  box-shadow: 0 20px 70px rgba(0, 0, 0, 0.25);
}

.resume-panel-head {
  display: flex;
  justify-content: space-between;
  align-items: start;
  gap: 20px;
  margin-bottom: 18px;
}

.resume-kicker {
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--muted-warm);
  margin-bottom: 10px;
}

.resume-panel h3 {
  font-size: 34px;
  line-height: 1.1;
  color: #ffffff;
}

.resume-summary {
  color: #b8bfd9;
  font-size: 17px;
  line-height: 1.8;
  max-width: 900px;
  margin-bottom: 28px;
}

.resume-story-grid,
.education-grid,
.badge-grid,
.cert-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}

.resume-story-card,
.timeline-card,
.education-card,
.badge-card,
.cert-card {
  padding: 22px;
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  transition: transform 0.25s ease, border-color 0.25s ease, background 0.25s ease;
}

.resume-story-card:hover,
.timeline-card:hover,
.education-card:hover,
.badge-card:hover,
.cert-card:hover {
  transform: translateY(-4px);
  border-color: rgba(255,122,26,0.32);
  background: rgba(255,122,26,0.06);
}

.story-label,
.badge-type,
.cert-meta {
  display: inline-flex;
  margin-bottom: 10px;
  font-size: 12px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #8fa2ff;
}

.resume-story-card p,
.education-card p,
.badge-card p,
.cert-card p {
  color: #c6cadb;
  line-height: 1.7;
}

.timeline-list {
  display: grid;
  gap: 16px;
}

.timeline-top {
  display: flex;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 14px;
}

.timeline-top h4,
.spotlight-card h4,
.education-card h4,
.badge-card h4,
.cert-card h3 {
  color: #ffffff;
  font-size: 20px;
  margin-bottom: 6px;
}

.timeline-top p,
.spotlight-card p,
.education-card span,
.cert-card p {
  color: #b8bfd9;
  line-height: 1.6;
}

.timeline-pill {
  padding: 8px 12px;
  border-radius: 999px;
  font-size: 12px;
  background: rgba(255,122,26,0.12);
  color: #cdd7ff;
  white-space: nowrap;
  height: fit-content;
}

.timeline-card ul {
  padding-left: 18px;
  color: #d7daf0;
  line-height: 1.7;
}

.timeline-card li + li {
  margin-top: 8px;
}

.spotlight-grid {
  display: grid;
  gap: 16px;
}

.spotlight-card {
  display: grid;
  grid-template-columns: 170px 1fr;
  gap: 18px;
  padding: 18px;
  border-radius: 22px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.spotlight-card img {
  width: 100%;
  height: 100%;
  min-height: 140px;
  object-fit: cover;
  border-radius: 16px;
}

.spotlight-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 14px;
}

.spotlight-tags span {
  padding: 8px 12px;
  border-radius: 999px;
  background: rgba(255,122,26,0.12);
  color: #dbe1ff;
  font-size: 12px;
}

.resume-stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
  margin-top: 20px;
}

.resume-stat {
  padding: 18px;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255,122,26,0.12);
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.resume-stat strong {
  font-size: 24px;
  color: #ffffff;
}

.resume-stat span {
  color: #b8bfd9;
  font-size: 13px;
}

.btn-mini {
  padding: 12px 18px;
  font-size: 14px;
  border-radius: 999px;
}

/* Certification Section */
.certification {
  background: linear-gradient(135deg, rgba(20,12,10,0.06) 0%, rgba(20,12,10,0.08) 100%);
}

.cert-carousel {
  display: grid;
  grid-template-columns: 1.65fr 1fr;
  gap: 20px;
  align-items: stretch;
}

.cert-preview {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  border-radius: 18px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.12);
  box-shadow: 0 18px 44px rgba(0, 0, 0, 0.28);
  min-height: 420px;
  background: rgba(12, 20, 48, 0.6);
}

.cert-image {
  width: 100%;
  height: auto;
  max-height: 520px;
  border-radius: 12px;
  object-fit: contain;
  display: block;
  background: linear-gradient(140deg, rgba(255, 255, 255, 0.08), rgba(8, 15, 35, 0.8));
}

.cert-nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 42px;
  height: 42px;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background: rgba(7, 13, 31, 0.78);
  backdrop-filter: blur(6px);
  color: #ffffff;
  font-size: 30px;
  line-height: 1;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.2s ease, background 0.2s ease;
}

.cert-nav:hover {
  transform: translateY(-50%) scale(1.05);
  background: rgba(255,122,26,0.14);
}

.cert-nav-prev {
  left: 12px;
}

.cert-nav-next {
  right: 12px;
}

.cert-details-card {
  padding: 24px;
  border-radius: 18px;
  background: rgba(15, 22, 50, 0.75);
  border: 1px solid rgba(255,122,26,0.22);
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.22);
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.cert-details-card h3 {
  font-size: 25px;
  line-height: 1.3;
  color: #ffffff;
  margin-bottom: 8px;
}

.cert-issuer {
  color: #d2d8ff;
  font-weight: 600;
  margin-bottom: 10px;
}

.cert-context {
  color: #b7bfdc;
  line-height: 1.7;
  margin-bottom: 16px;
}

.cert-counter {
  display: inline-flex;
  padding: 7px 12px;
  border-radius: 999px;
  border: 1px solid rgba(143, 162, 255, 0.45);
  color: #dfe4ff;
  font-size: 13px;
}

.cert-thumbnails {
  grid-column: 1 / -1;
  display: flex;
  gap: 10px;
  overflow-x: auto;
  padding: 2px 2px 6px;
  scroll-snap-type: x mandatory;
}

.cert-thumb {
  flex: 0 0 120px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.03);
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  padding: 0;
  scroll-snap-align: start;
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.cert-thumb img {
  width: 100%;
  height: 84px;
  object-fit: cover;
  display: block;
}

.cert-thumb:hover,
.cert-thumb.active {
  transform: translateY(-3px);
  border-color: rgba(143, 162, 255, 0.75);
  box-shadow: 0 10px 22px rgba(85, 109, 255, 0.18);
}

.awards-strip {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
  margin-top: 24px;
}

.award-chip {
  padding: 10px 14px;
  border-radius: 999px;
  background: rgba(255,122,26,0.12);
  border: 1px solid rgba(255,122,26,0.22);
  color: #dfe4ff;
  font-size: 13px;
}

/* About Section */
.about {
  background: linear-gradient(135deg, rgba(12,8,6,0.02) 0%, rgba(12,8,6,0.04) 100%);
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
  border: 1px solid rgba(255,122,26,0.12);
  border-radius: 16px;
  transition: all 0.3s ease;
  margin-right: -50px;
  height: 100%;
  width: 78%;
}

.about-card:hover {
  background: rgba(255,122,26,0.06);
  border-color: rgba(255,122,26,0.28);
  transform: translateY(-5px);
}

.about-card h3 {
  font-size: 30px;
  margin-bottom: 20px;
  color: var(--primary-1);
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
  border: 1px solid rgba(255,122,26,0.22);
  transition: all 0.3s ease;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  height: 100%;
  width: 100%;
  margin-left: -50px;
}

.about-image:hover {
  transform: translateY(-8px);
  border-color: rgba(255,122,26,0.36);
  box-shadow: 0 20px 60px rgba(255,122,26,0.12);
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
  background: linear-gradient(135deg, rgba(12,8,6,0.02) 0%, rgba(12,8,6,0.04) 100%);
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
  border: 1px solid rgba(255,122,26,0.12);
  border-radius: 16px;
  transition: all 0.3s ease;
}

.skill-category:hover {
  background: rgba(255,122,26,0.06);
  border-color: rgba(255,122,26,0.28);
  transform: translateY(-5px);
}

.category-title {
  font-size: 22px;
  margin-bottom: 25px;
  color: var(--primary-1);
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.skill-tag {
  padding: 10px 18px;
  background: rgba(255,122,26,0.12);
  border: 1px solid rgba(255,122,26,0.28);
  border-radius: 20px;
  font-size: 14px;
  color: #e0e0e0;
  transition: all 0.3s ease;
  cursor: default;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.skill-icon {
  width: 16px;
  height: 16px;
  object-fit: contain;
  flex-shrink: 0;
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

.lemi-toggle {
  position: fixed;
  right: 24px;
  bottom: 24px;
  z-index: 1300;
  border: none;
  border-radius: 999px;
  background: linear-gradient(135deg, var(--primary-1) 0%, var(--primary-2) 100%);
  color: #ffffff;
  padding: 12px 18px;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-weight: 700;
  font-size: 14px;
  cursor: pointer;
  box-shadow: 0 14px 36px rgba(80, 98, 212, 0.45);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.lemi-toggle:hover {
  transform: translateY(-2px);
  box-shadow: 0 18px 40px rgba(80, 98, 212, 0.55);
}

.lemi-toggle-icon {
  font-size: 17px;
  line-height: 1;
}

.lemi-chat {
  position: fixed;
  right: 24px;
  bottom: 84px;
  width: min(370px, calc(100vw - 32px));
  max-height: min(620px, calc(100vh - 120px));
  border-radius: 18px;
  border: 1px solid rgba(120, 140, 255, 0.4);
  background: rgba(9, 12, 28, 0.92);
  backdrop-filter: blur(12px);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
  z-index: 1300;
  display: grid;
  grid-template-rows: auto 1fr auto auto;
  overflow: hidden;
}

.lemi-header {
  display: flex;
  align-items: start;
  justify-content: space-between;
  gap: 10px;
  padding: 16px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.3), rgba(118, 75, 162, 0.3));
}

.lemi-kicker {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: #d5dcff;
  margin-bottom: 6px;
}

.lemi-header h3 {
  font-size: 20px;
  color: #ffffff;
}

.lemi-close {
  width: 30px;
  height: 30px;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.22);
  background: rgba(255, 255, 255, 0.06);
  color: #ffffff;
  cursor: pointer;
}

.lemi-messages {
  padding: 14px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.lemi-message {
  max-width: 92%;
  border-radius: 14px;
  padding: 11px 12px;
  line-height: 1.6;
  font-size: 13px;
}

.lemi-message p {
  margin: 0;
  color: #eef1ff;
}

.lemi-message.assistant {
  align-self: flex-start;
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.12);
}

.lemi-message.user {
  align-self: flex-end;
  background: rgba(102, 126, 234, 0.35);
  border: 1px solid rgba(152, 168, 255, 0.35);
}

.lemi-typing p {
  color: #cad4ff;
  font-style: italic;
}

.lemi-quick-asks {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  padding: 10px 14px 0;
}

.lemi-quick-btn {
  border: 1px solid rgba(115, 137, 255, 0.42);
  background: rgba(102, 126, 234, 0.14);
  color: #dfe5ff;
  border-radius: 999px;
  padding: 7px 10px;
  font-size: 11px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.lemi-quick-btn:hover {
  background: rgba(102, 126, 234, 0.25);
}

.lemi-form {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 10px;
  padding: 12px 14px 14px;
}

.lemi-input {
  width: 100%;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  background: rgba(0, 0, 0, 0.3);
  color: #ffffff;
  padding: 10px 12px;
  font-size: 13px;
  outline: none;
}

.lemi-input:focus {
  border-color: rgba(130, 150, 255, 0.95);
}

.lemi-send {
  border: none;
  border-radius: 12px;
  background: linear-gradient(135deg, var(--primary-1) 0%, rgba(255,122,26,0.9) 100%);
  color: #ffffff;
  font-weight: 700;
  padding: 0 16px;
  cursor: pointer;
  transition: opacity 0.2s ease;
}

.lemi-send:disabled {
  opacity: 0.55;
  cursor: not-allowed;
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

  .hero-content {
    margin-left: 0;
  }

  .profile-image-wrapper {
    margin-left: 0;
  }

  .profile-image-wrapper {
    transform: translateX(0) !important;
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

  .cert-carousel {
    grid-template-columns: 1fr;
  }

  .cert-preview {
    min-height: 300px;
  }
}

@media (max-width: 768px) {
  .navbar {
    height: 70px;
  }

  .nav-toggle {
    display: inline-flex;
  }

  .nav-links {
    display: none;
  }

  .mobile-menu {
    display: flex;
    position: fixed;
    top: 70px;
    right: 12px;
    left: 12px;
    background: rgba(6,6,6,0.95);
    border-radius: 12px;
    padding: 12px;
    flex-direction: column;
    gap: 8px;
    z-index: 1250;
    box-shadow: 0 12px 40px rgba(0,0,0,0.6);
  }

  .mobile-menu a {
    color: #e0e0e0;
    padding: 12px 10px;
    text-decoration: none;
    border-radius: 8px;
    background: rgba(255,255,255,0.02);
    text-align: center;
    font-weight: 700;
  }

  .mobile-menu a:active { transform: translateY(1px); }

  /* Keep social dropdown visible on mobile (right side) */
  .social-dropdown { display: flex; right: 16px; top: 50%; transform: translateY(-50%); }

  /* position hamburger and logo to the left */
  .nav-toggle { left: 12px; right: auto; }
  .logo { left: 56px; }
  .logo-text { display: inline-block; font-size: 14px; }

  /* Tighter hero spacing on small devices */
  .hero { padding: 80px 16px 40px; }

  /* Reduce profile image size and center it */
  .profile-image-wrapper {
    width: 92%;
    height: 240px;
    margin-top: 30px;
    padding: 8px;
    border-radius: 16px;
    margin-left: auto;
    margin-right: auto;
    transform: translateX(0) !important;
  }

  .profile-image { border-radius: 12px; }

  /* Keep bubble centered and unclipped on mobile. */
  .profile-chat { top: 8px; right: 0; left: 0; }
  .chat-bubble { font-size: 12px; padding: 8px 10px; max-width: 100%; }
  .typing-text { animation: none; }


  .lemi-toggle:hover { box-shadow: 0 16px 40px rgba(0,0,0,0.55); }

  /* Make hero buttons full width for easier tapping */
  .hero-actions { flex-direction: row; flex-wrap: nowrap; gap: 10px; width: 100%; }
  .btn-primary, .btn-secondary { width: auto; flex: 1 1 0; min-width: 0; padding: 12px 10px; font-size: 13px; white-space: nowrap; }

  /* Ensure scroll indicator remains visible and not overlapping */
  .scroll-indicator { bottom: 18px; }

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
    margin-left: 0;
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
    flex-direction: row;
    flex-wrap: nowrap;
    width: 100%;
    gap: 10px;
  }

  .btn-primary, .btn-secondary {
    width: auto;
    flex: 1 1 0;
    min-width: 0;
    padding: 12px 10px;
    font-size: 13px;
    border-radius: 10px;
    white-space: nowrap;
  }

  .hero-3d {
    height: auto;
    min-height: 0;
    margin-top: 10px;
    margin-bottom: 6px;
    align-items: center;
    justify-content: center;
    width: 100%;
  }

  .profile-image-wrapper {
    width: min(100%, 340px);
    aspect-ratio: 1 / 1.05;
    height: auto;
    margin-top: 0;
    margin-left: auto;
    margin-right: auto;
    transform: translateX(0) !important;
  }

  .profile-image {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  .profile-chat {
    top: 8px;
    left: 0;
    right: 0;
    width: 100%;
    display: flex;
    justify-content: center;
    transform: none;
  }

  .chat-bubble {
    max-width: 100%;
  }

  .resume-shell {
    grid-template-columns: 1fr;
    gap: 18px;
  }

  .resume-tabs {
    flex-direction: row;
    overflow-x: auto;
    position: static;
    top: auto;
    padding-bottom: 6px;
    scroll-snap-type: x proximity;
  }

  .resume-tab {
    flex: 0 0 auto;
    min-width: 180px;
  }

  .resume-panel {
    padding: 24px;
    border-radius: 22px;
  }

  .resume-panel-head {
    flex-direction: column;
    align-items: flex-start;
  }

  .resume-panel h3 {
    font-size: 26px;
  }

  .resume-summary {
    font-size: 15px;
    margin-bottom: 20px;
  }

  .resume-story-grid,
  .education-grid,
  .badge-grid {
    grid-template-columns: 1fr;
  }

  .spotlight-card {
    grid-template-columns: 1fr;
  }

  .spotlight-card img {
    min-height: 180px;
  }

  .timeline-top {
    flex-direction: column;
  }

  .timeline-pill {
    align-self: flex-start;
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

  .cert-nav {
    width: 36px;
    height: 36px;
    font-size: 24px;
  }

  .cert-thumb {
    flex-basis: 96px;
  }

  .cert-thumb img {
    height: 70px;
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

  .lemi-chat {
    right: 16px;
    bottom: 74px;
    width: min(360px, calc(100vw - 24px));
  }

  .lemi-toggle {
    right: 16px;
    bottom: 16px;
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
    display: inline-block;
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
    height: auto;
    min-height: 0;
    margin-top: 0;
    margin-bottom: 4px;
    align-items: center;
    justify-content: center;
    width: 100%;
  }

  .profile-image-wrapper {
    width: min(100%, 290px);
    aspect-ratio: 1 / 1.08;
    height: auto;
    margin-top: 0;
    margin-left: auto;
    margin-right: auto;
  }

  .profile-image {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  .profile-chat {
    top: 6px;
    left: 0;
    right: 0;
    width: 100%;
    display: flex;
    justify-content: center;
    transform: none;
  }

  .chat-bubble {
    max-width: 100%;
    font-size: 11px;
  }

  .resume-shell {
    gap: 14px;
  }

  .resume-tabs {
    gap: 10px;
  }

  .resume-tab {
    min-width: 150px;
    padding: 12px 14px;
    border-radius: 14px;
  }

  .resume-tab-index {
    width: 30px;
    height: 30px;
    font-size: 11px;
  }

  .resume-panel {
    padding: 18px;
    border-radius: 18px;
  }

  .resume-panel h3 {
    font-size: 22px;
  }

  .resume-summary {
    font-size: 14px;
  }

  .spotlight-card {
    gap: 14px;
    padding: 14px;
  }

  .spotlight-card img {
    min-height: 150px;
  }

  .timeline-top h4,
  .spotlight-card h4,
  .education-card h4,
  .badge-card h4,
  .cert-card h3 {
    font-size: 18px;
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

  .lemi-chat {
    right: 10px;
    bottom: 70px;
  }

  .lemi-toggle {
    right: 10px;
    bottom: 10px;
    padding: 11px 14px;
  }

  .lemi-toggle-label {
    font-size: 12px;
  }
}
</style>

<!-- Global variables: keep unscoped so they apply across the app -->
<style>
:root {
  --bg-dark: #0b0b0b;
  --bg-accent: #15100d;
  --primary-1: #ff7a1a;
  --primary-2: #ff4d00;
  --muted-warm: #bfa48b;
  --glass-border: rgba(255,120,40,0.12);
  --primary-glow: rgba(255,122,26,0.28);
}
</style>
