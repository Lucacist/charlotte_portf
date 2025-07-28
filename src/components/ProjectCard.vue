<template>
  <div class="project-card" @click="navigateToProject">
    <div class="project-image">
      <img :src="project.image" :alt="project.title" />
      <div v-if="project.status" class="status-badge" :class="project.status">
        {{ getStatusLabel(project.status) }}
      </div>
    </div>
    <div class="project-info">
      <h3>{{ project.title }}</h3>
      <p>{{ project.shortDescription }}</p>
      <div class="project-technologies">
        <div v-for="(tech, index) in project.technologies" :key="index" class="tech-logo">
          <img :src="tech.logo" :alt="tech.name" :title="tech.name" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProjectCard',
  props: {
    project: {
      type: Object,
      required: true
    }
  },
  methods: {
    navigateToProject() {
      this.$router.push({ 
        name: 'project-detail', 
        params: { id: this.project.id } 
      });
    },
    getStatusLabel(status) {
      switch(status) {
        case 'completed': return 'Terminé';
        case 'in-progress': return 'En cours';
        case 'planned': return 'Planifié';
        default: return status;
      }
    }
  }
}
</script>

<style scoped>
.project-card {
  background-color: #ffffff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
}

.project-image {
  height: 200px;
  overflow: hidden;
  position: relative;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-info {
  padding: 1.5rem;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}

.project-info h3 {
  margin-top: 0;
  margin-bottom: 0.5rem;
  font-size: 1.25rem;
  color: #333;
}

.project-info p {
  color: #666;
  margin-bottom: 1rem;
  flex-grow: 1;
}

.project-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: auto;
  justify-content: center;
}

.tech-logo {
  display: flex;
  align-items: center;
  justify-content: center;
}

.tech-logo img {
  width: 30px;
  height: 30px;
  object-fit: contain;
  transition: transform 0.2s ease;
}

.tech-logo img:hover {
  transform: scale(1.2);
}

.status-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.7rem;
  font-weight: 600;
  z-index: 10;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.status-badge.completed {
  background-color: #d1fae5;
  color: #047857;
}

.status-badge.in-progress {
  background-color: #fef3c7;
  color: #b45309;
}

.status-badge.planned {
  background-color: #e0e7ff;
  color: #4338ca;
}
</style>
