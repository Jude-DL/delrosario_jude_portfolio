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
    </div>
  </div>
</template>

<script setup lang="ts">
interface Project {
  title: string
  description: string
  image: string
  tags: string[]
  link: string
}

interface Props {
  project: Project
}

defineProps<Props>()
</script>

<style scoped>
.project-card {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-5px);
  border-color: rgba(0, 255, 136, 0.5);
  background: rgba(0, 255, 136, 0.1);
}

.project-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
  background: linear-gradient(135deg, rgba(0, 255, 136, 0.2), rgba(138, 43, 226, 0.2));
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
  background: rgba(0, 255, 136, 0.2);
  color: #00ff88;
  border-radius: 20px;
  border: 1px solid rgba(0, 255, 136, 0.3);
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  color: #00ff88;
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
</style>
