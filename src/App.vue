<script setup>
import NavBar from './components/NavBar.vue'
</script>

<template>
  <div class="app">
    <NavBar />
    <main class="main-content">
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>
    <!-- 
    <footer class="footer">
      <div class="footer-content">
        <p>&copy; {{ new Date().getFullYear() }} Charlotte. Tous droits réservés.</p>
      </div>
    </footer>-->
  </div>
</template>

<style>
/* Reset CSS et styles globaux */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  line-height: 1.6;
}

h1, h2, h3, h4, h5, h6 {
  margin-bottom: 1rem;
  font-weight: 700;
  line-height: 1.2;
}

h1 {
  font-size: 2.5rem;
}

h2 {
  font-size: 2rem;
}

p {
  margin-bottom: 1rem;
}

img {
  max-width: 100%;
}

/* Layout styles */
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
}

.main-content {
 display: flex;
 flex-direction: column;
 min-height: 100%;
 width: 100%;
 margin-top: 3.5rem;
}

.footer {
  padding: 2rem 0;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  text-align: center;
}

/* Transitions de page */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
