<template>
  <div class="project-card" :class="'card-color-' + (index % 10)" @click="navigateToProject">
    <div class="project-image">
      <img :src="project.cardImage || project.image" :alt="project.title" />
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
    <div class="project-overlay">
      <span>Voir le projet</span>
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
    },
    index: {
      type: Number,
      default: 0
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
  overflow: hidden;
  transition: transform 0.3s ease;
  cursor: pointer;
  height: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  padding: 1rem;
  gap: 1rem;
}

.card-color-0 {
  background-color: #ffffff; /* Blanc */
}

.card-color-1 {
  background-color: #f7f7f7; /* Gris très clair */
}

.card-color-2 {
  background-color: #f9f9f9; /* Blanc cassé */
}

.card-color-3 {
  background-color: #fcfcfc; /* Blanc légèrement grisé */
}

.card-color-4 {
  background-color: #f0f0f0; /* Gris clair */
}

.card-color-5 {
  background-color: #f5f5f5; /* Gris très pâle */
}

.card-color-6 {
  background-color: #fafafa; /* Blanc presque pur */
}

.card-color-7 {
  background-color: #f8f8f8; /* Gris très léger */
}

.card-color-8 {
  background-color: #fdfdfd; /* Blanc légèrement cassé */
}

.card-color-9 {
  background-color: #f2f2f2; /* Gris pâle */
}

.project-image {
  height: 200px;
  overflow: hidden;
  position: relative;
}

.project-image img {
  height: 100%;
  object-fit: cover;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: flex-end;
  padding-bottom: 3rem;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-overlay span {
  color: white;
  font-size: 2.2rem;
  font-weight: 600;
  transform: translateY(100px);
  transition: transform 0.3s ease;
  font-family: 'Titan One', sans-serif;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-card:hover .project-overlay span {
  transform: translateY(0);
}


.project-info {
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
