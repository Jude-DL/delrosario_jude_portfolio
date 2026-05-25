<template>
  <div class="project-card">
    <div class="project-image">
      <img :src="project.image" :alt="project.title" />
    </div>
    <div class="project-content">
      <h3 class="project-title">{{ project.title }}</h3>
      <p class="project-description">{{ project.description }}</p>
      <div class="project-tags">
        <span v-for="tag in project.tags" :key="tag" class="tag">{{ tag }}</span>
      </div>
        <div class="project-actions">
          <a
            v-if="project.link && project.deployed !== false"
            :href="project.link"
            class="project-link"
            target="_blank"
            rel="noopener noreferrer"
          >
            View
            <span class="arrow">→</span>
          </a>

          <button
            v-else-if="project.link && project.deployed === false"
            class="project-link"
            @click.prevent="showWarning = true"
            aria-haspopup="dialog"
          >
            View
            <span class="arrow">→</span>
          </button>
        </div>

        <div v-if="showWarning" class="pc-modal" role="dialog" aria-modal="true">
          <div class="pc-modal-card">
            <h3>Not Deployed</h3>
            <p>This project is not deployed yet. You can still view details in the portfolio but the live demo is unavailable.</p>
            <div class="pc-modal-actions">
              <button class="pc-close" @click="showWarning = false">Close</button>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script setup lang="ts">

import { ref } from 'vue'

interface Project {
  title: string
  description: string
  image: string
  tags: string[]
  link: string
  deployed?: boolean
}

interface Props {
  project: Project
}

defineProps<Props>()

const showWarning = ref(false)
</script>

<style scoped>
.project-card {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid var(--glass-border);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
}

.project-card:hover {
  transform: translateY(-5px);
  border-color: var(--primary-glow);
  background: rgba(255,122,26,0.06);
}

.project-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
  background: linear-gradient(135deg, rgba(255,122,26,0.08), rgba(255,77,0,0.06));
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-content {
  padding: 24px;
  padding-bottom: 72px;
}

.project-title {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 12px;
  color: #ffffff;
}

.project-description {
  font-size: 14px;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 16px;
  line-height: 1.6;
}

.project-tags {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.tag {
  font-size: 12px;
  padding: 4px 12px;
  background: rgba(255,122,26,0.06);
  color: var(--primary-1);
  border-radius: 20px;
  border: 1px solid rgba(255,122,26,0.14);
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  color: var(--primary-1);
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  transition: gap 0.3s ease;
}

.project-link:hover {
  gap: 12px;
}

.arrow {
  transition: transform 0.3s ease;
}

.project-link:hover .arrow {
  transform: translateX(4px);
}

.project-actions {
  position: absolute;
  right: 20px;
  bottom: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.project-actions .project-link {
  margin: 0;
  padding: 12px 18px;
  min-width: 96px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(180deg, rgba(255,122,26,0.12), rgba(255,77,0,0.06));
  border-radius: 999px;
  border: 1px solid rgba(255,122,26,0.16);
  color: #fff;
  font-weight: 700;
  box-shadow: 0 10px 28px rgba(255,122,26,0.06), inset 0 -6px 18px rgba(0,0,0,0.25);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.project-actions .project-link .arrow {
  margin-left: 8px;
  transition: transform 0.18s ease;
}

.project-actions .project-link:hover {
  transform: translateY(-6px);
  box-shadow: 0 18px 40px rgba(255,122,26,0.12), inset 0 -6px 18px rgba(0,0,0,0.28);
}

.project-actions .project-link:hover .arrow {
  transform: translateX(6px);
}

.pc-modal {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(2,6,23,0.6);
  z-index: 2000;
}
.pc-modal-card {
  background: #071028;
  padding: 20px;
  border-radius: 12px;
  max-width: 420px;
  width: 90%;
  color: #e6eef8;
  border: 1px solid rgba(255,255,255,0.04);
  box-shadow: 0 12px 40px rgba(0,0,0,0.6);
}
.pc-modal-card h3{margin:0 0 8px}
.pc-modal-card p{color:rgba(255,255,255,0.7);margin:0 0 12px}
.pc-modal-actions{display:flex;justify-content:flex-end}
.pc-close{background:transparent;border:1px solid rgba(255,255,255,0.05);padding:8px 12px;border-radius:8px;color:#e6eef8;cursor:pointer}

</style>
