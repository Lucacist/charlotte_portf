<template>
  <div class="project-detail-container" v-if="project">
    <div class="back-button">
        <button @click="goBack">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M10.5 19.5 3 12m0 0 7.5-7.5M3 12h18"
            />
          </svg>
          Retour aux projets
        </button>
      </div>
    <div class="project-header">
      <div class="title-status-container">
        <h1>{{ project.title }}</h1>
        <div class="status-badge" :class="project.status">
          {{ getStatusLabel(project.status) }}
        </div>
      </div>
      <div class="project-technologies">
        <div
          v-for="(tech, index) in project.technologies"
          :key="index"
          class="tech-logo"
        >
          <img :src="tech.logo" :alt="tech.name" :title="tech.name" />
        </div>
      </div>
    </div>

    <div class="project-content">
      <div class="project-image">
        <img :src="project.image" :alt="project.title" />
      </div>

      <div class="project-description">
        <h2>Description</h2>
        <div class="description-text">
          <p v-for="(paragraph, index) in formattedDescription" :key="index">
            {{ paragraph }}
          </p>
        </div>

        <div class="project-links">
          <a
            v-if="project.link"
            :href="project.link"
            target="_blank"
            class="project-button"
          >
          <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <circle cx="12" cy="12" r="10"></circle>
              <line x1="2" y1="12" x2="22" y2="12"></line>
              <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10a15.3 15.3 0 0 1 4-10z"></path>
            </svg>
            <span>Voir le projet</span>
          </a>
          <a
            v-if="project.github"
            :href="project.github"
            target="_blank"
            class="project-button github"
          >
          <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path
                d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
              ></path>
            </svg>
            <span>GitHub</span>
          </a>
          <a
            v-if="project.codeDownload"
            :href="project.codeDownload"
            target="_blank"
            class="project-button code"
          >
          <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
              <polyline points="14 2 14 8 20 8"></polyline>
              <line x1="16" y1="13" x2="8" y2="13"></line>
              <line x1="16" y1="17" x2="8" y2="17"></line>
              <polyline points="10 9 9 9 8 9"></polyline>
            </svg>
            <span>Télécharger le code</span>
          </a>
          <a
            v-if="project.documentation"
            :href="project.documentation"
            target="_blank"
            class="project-button doc"
          >
          <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
              <polyline points="14 2 14 8 20 8"></polyline>
              <line x1="16" y1="13" x2="8" y2="13"></line>
              <line x1="16" y1="17" x2="8" y2="17"></line>
              <polyline points="10 9 9 9 8 9"></polyline>
            </svg>
            <span>Documentation PDF</span>
          </a>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="not-found">
    <h2>Projet non trouvé</h2>
    <button @click="goBack">Retour aux projets</button>
  </div>
</template>

<script>
import projectsData from "../data/projects.json";

export default {
  name: "ProjectDetailView",
  data() {
    return {
      project: null,
    };
  },
  computed: {
    formattedDescription() {
      if (!this.project || !this.project.description) return [];
      return this.project.description
        .split("\n\n")
        .filter((paragraph) => paragraph.trim() !== "");
    },
  },
  created() {
    const projectId = parseInt(this.$route.params.id);
    this.project = projectsData.find((p) => p.id === projectId);
  },
  methods: {
    goBack() {
      this.$router.push({ name: "projects" });
    },
    getStatusLabel(status) {
      switch(status) {
        case 'completed': return 'Terminé';
        case 'in-progress': return 'En cours';
        case 'planned': return 'Planifié';
        default: return status;
      }
    }
  },
};
</script>

<style scoped>
.project-detail-container {
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem;
}

.project-header {
  margin-bottom: 2rem;
  text-align: center;
}

.title-status-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.project-header h1 {
  font-size: 2.5rem;
  margin: 0;
  color: #333;
}

.status-badge {
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
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

.project-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-top: 1rem;
}

.tech-logo {
  display: flex;
  align-items: center;
  justify-content: center;
}

.tech-logo img {
  width: 40px;
  height: 40px;
  object-fit: contain;
  transition: transform 0.2s ease;
}

.tech-logo img:hover {
  transform: scale(1.2);
}

.project-content {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-bottom: 2rem;
}

.project-image img {
  width: 80%;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.project-description h2 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #333;
  text-align: left;
}

.project-description .description-text p {
  line-height: 1.6;
  color: #444;
  margin-bottom: 1.5rem;
  text-align: justify;
}

.description-text {
  margin-bottom: 1.5rem;
}


.project-button {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  border: 1px solid var(--border-color);
  color: var(--text-color);
}

.project-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.github-button svg,
.download-button svg,
.site-button svg {
  width: 20px;
  height: 20px;
}

.project-links {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-top: 2rem;
}

.back-button {
  text-align: center;
  display: flex;
  
}

.project-button svg , .back-button button svg {
  width: 20px;
}

.back-button button {
  padding: 0.75rem 1.5rem;
  background-color: transparent;
  border: none;
  border-radius: 4px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.3s ease;
  display: flex;
  gap: 0.5rem;
  align-items: center;
  justify-content: center;
}

.not-found {
  text-align: center;
  padding: 3rem;
}

.not-found h2 {
  margin-bottom: 1.5rem;
  color: #333;
}

@media (max-width: 768px) {
  .project-content {
    grid-template-columns: 1fr;
  }

  .project-header h1 {
    font-size: 2rem;
  }
}
</style>
