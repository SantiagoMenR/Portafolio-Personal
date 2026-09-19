<template>
  <div class="app-container">
    <NavBar />
    
    <main>
      <HeroSection />
      <TechStackSection />
      <ProjectsSection />
      <EducationSection />
      <ContactSection />
    </main>

    <footer class="footer">
      <div class="container">
        <p>© Copyright <strong>Santiago Mendoza Rivera</strong>. Todos los derechos reservados.</p>
      </div>
    </footer>
    
    <a href="#" class="btn-scroll-top" :class="{ 'visible': showScrollTop }" @click.prevent="scrollToTop">
      <i class="fa-solid fa-arrow-up"></i>
    </a>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Components
import NavBar from './components/NavBar.vue';
import HeroSection from './components/HeroSection.vue';
import TechStackSection from './components/TechStackSection.vue';
import ProjectsSection from './components/ProjectsSection.vue';
import EducationSection from './components/EducationSection.vue';
import ContactSection from './components/ContactSection.vue';

const showScrollTop = ref(false);

const handleScroll = () => {
  showScrollTop.value = window.scrollY > 500;
};

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style>
@import './assets/main.css';
@import '@fortawesome/fontawesome-free/css/all.min.css';

.footer {
  text-align: center;
  padding: 2rem 0;
  background: var(--bg-secondary);
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.footer p {
  color: var(--text-secondary);
  font-size: 0.9rem;
}

.footer strong {
  color: var(--accent-primary);
}

.designer {
  margin-top: 0.5rem;
  font-size: 0.8rem !important;
  color: var(--text-muted) !important;
}

.btn-scroll-top {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 50px;
  height: 50px;
  background: var(--accent-primary);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  opacity: 0;
  visibility: hidden;
  transform: translateY(20px);
  transition: all 0.3s ease;
  z-index: 999;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
}

.btn-scroll-top.visible {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.btn-scroll-top:hover {
  background: var(--accent-secondary);
  transform: translateY(-5px);
}
</style>
