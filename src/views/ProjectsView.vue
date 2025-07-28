<template>
  <div class="projects-container">
    <div class="projects-grid">
      <div v-for="project in projects" :key="project.id" class="project-item">
        <ProjectCard :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
import ProjectCard from '../components/ProjectCard.vue';
import projectsData from '../data/projects.json';

export default {
  name: 'ProjectsView',
  components: {
    ProjectCard
  },
  data() {
    return {
      projects: projectsData
    };
  }
}
</script>

<style scoped>
.projects-container {
    width: 100%;
    margin-top: 2rem;
}

.section-title {
  text-align: center;
  margin-bottom: 2rem;
  font-size: 2.5rem;
  color: #333;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
}

.project-item {
  height: 100%;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1.5rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
}

@media (max-width: 480px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
