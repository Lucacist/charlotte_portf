<template>
  <nav class="navbar" :class="{ 'scrolled': scrolled }">
    <div class="navbar-container">
      <router-link to="/" class="logo"><img src="/images/logo.svg" alt="Logo"></router-link>
      
      <button class="menu-toggle" @click="toggleMenu" :class="{ 'active': menuOpen }" aria-label="Toggle menu">
        <span></span>
        <span></span>
      </button>
      
      <div class="nav-links" :class="{ 'active': menuOpen }">
        <router-link to="/" class="nav-link" @click="closeMenu">Accueil</router-link>
        <router-link to="/projects" class="nav-link" @click="closeMenu">Projets</router-link>
        <router-link to="/contact" class="nav-link" @click="closeMenu">Contact</router-link>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const scrolled = ref(false);
const menuOpen = ref(false);

// Fonction pour vérifier le défilement
function checkScroll() {
  scrolled.value = window.scrollY > 10;
}

// Fonction pour basculer le menu mobile
function toggleMenu() {
  menuOpen.value = !menuOpen.value;
  if (menuOpen.value) {
    document.body.style.overflow = 'hidden';
  } else {
    document.body.style.overflow = 'auto';
  }
}

// Fonction pour fermer le menu
function closeMenu() {
  if (menuOpen.value) {
    menuOpen.value = false;
    document.body.style.overflow = 'auto';
  }
}

// Ajouter l'écouteur d'événement au montage du composant
onMounted(() => {
  window.addEventListener('scroll', checkScroll);
  checkScroll(); // Vérifier l'état initial
});

// Supprimer l'écouteur d'événement lors du démontage du composant
onUnmounted(() => {
  window.removeEventListener('scroll', checkScroll);
});
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  padding: 1.5rem 0;
  transition: all 0.3s ease;
  background-color: transparent;
}

.navbar.scrolled {
  background-color: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 1rem 0;
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.navbar-container img {
  width: 90px;
}

.logo {
  font-size: 1.5rem;
  font-weight: 200;
  color: #42b883;
  text-decoration: none;
  transition: color 0.3s ease;
  font-family: "Oceanic-Medium", system-ui, Avenir, Helvetica, Arial, sans-serif;
}

.logo:hover {
  color: #3aa876;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-link {
  color: #333;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
  position: relative;
}

.nav-link:hover,
.router-link-active {
  color: #42b883;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #42b883;
  transition: width 0.3s ease;
}

.nav-link:hover::after,
.router-link-active::after {
  width: 100%;
}

.menu-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  width: 24px;
  height: 20px;
  position: relative;
  z-index: 1001;
}

.menu-toggle span {
  display: block;
  width: 100%;
  height: 2px;
  background-color: #333;
  transition: all 0.3s ease;
  border-radius: 50px;
}

/* Responsive design */
@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
  }
  
  .nav-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 70%;
    height: 100vh;
    background-color: white;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: right 0.3s ease;
    box-shadow: -5px 0 15px rgba(0, 0, 0, 0.1);
  }
  
  .nav-links.active {
    right: 0;
  }
  
  .menu-toggle.active span:nth-child(1) {
    transform: rotate(45deg) translateY(5px);
  }
  
  .menu-toggle.active span:nth-child(2) {
    transform: rotate(-45deg) translateY(-5px);
  }
}
</style>
