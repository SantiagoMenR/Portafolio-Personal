<template>
  <section id="projects" class="section projects-section">
    <div class="container">
      <h2 class="section-title">Mis Proyectos</h2>
      
      <div class="projects-grid">
        <div class="project-card glass-panel" v-for="(project, index) in projects" :key="index">
          <div class="project-image">
            <img :src="project.image" :alt="'Demo ' + project.title">
            <div class="project-overlay">
              <a v-if="project.github" :href="project.github" target="_blank" class="btn-link">
                <i class="fa-brands fa-github"></i> Ver Código
              </a>
              <a v-if="project.demo" :href="project.demo" target="_blank" class="btn-link btn-demo">
                <i class="fa-solid fa-external-link-alt"></i> Ver Demo
              </a>
            </div>
          </div>
          <div class="project-content">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="project-techs">
              <span v-for="(tech, tIndex) in project.techs" :key="tIndex">{{ tech }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

import ChatbotIA from '../assets/chatbot.png';
import LogiTrack from '../assets/logitrack.png';
import Cafeteria from '../assets/coffeshop.png';
import Tdn from '../assets/tdn.png';
import Exports from '../assets/exports.png';

gsap.registerPlugin(ScrollTrigger);

const projects = [
  {
    title: 'LogiTrack',
    description: 'Sistema de gestión de inventario y seguimiento de productos.',
    techs: ['Java', 'Spring Boot', 'PostgreSQL'],
    github: 'https://github.com/SantiagoMenR/LogiTrack_Proyecto_SpringBoot',
    image: LogiTrack
  },
  {
    title: 'Coffe Shop',
    description: 'Pagina web para una tienda de cafe, con Django como framework fullstack.',
    techs: ['Python', 'Django', 'PostgreSQL'],
    github: 'https://github.com/SantiagoMenR/Sistema_Gestion_Cafeteria',
    image: Cafeteria
  },
  {
    title: 'Chatbot Experto en Transporte',
    description: 'Chatbot experto en transporte, con Python y Flask para el backend y HTML y CSS para el frontend.',
    techs: ['Python', 'Flask', 'HTML', 'CSS', 'JavaScript'],
    github: 'https://github.com/SantiagoMenR/Chatbot_IA',
    image: ChatbotIA
  },
  {
    title: 'Exports',
    description: 'Plataforma para la gestión social y deportiva de escenarios deportivos.',
    techs: ['Vue.js', 'Spring Boot', 'PostgreSQL', 'Docker'],
    demo: 'https://playexports.com',
    image: Exports
  },
  {
    title: 'Marketplace para Niños',
    description: 'Marketplace interactivo con integración de IA (Gemini) para búsqueda vectorial y chatbot.',
    techs: ['Vue.js', 'Spring Boot', 'PostgreSQL', 'Docker', 'Gemini AI'],
    github: 'https://github.com/SantiagoMenR/tdn-api',
    image: Tdn
  }
];

onMounted(() => {
  // Title Animation
  gsap.fromTo('.projects-section .section-title', 
    { y: 50, opacity: 0 },
    { 
      y: 0, 
      opacity: 1, 
      duration: 0.8,
      scrollTrigger: {
        trigger: '.projects-section',
        start: 'top 80%',
      }
    }
  );

  // Cards stagger animation
  gsap.fromTo('.project-card', 
    { y: 60, opacity: 0 },
    { 
      y: 0, 
      opacity: 1, 
      duration: 0.8,
      stagger: 0.15,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '.projects-grid',
        start: 'top 80%',
      }
    }
  );
});
</script>

<style scoped>
.projects-section {
  background-color: var(--bg-primary);
}

.projects-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 2.5rem;
}

.project-card {
  width: calc((100% - 5rem) / 3);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.4s ease;
  background: rgba(27, 16, 18, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

@media (max-width: 1024px) {
  .project-card {
    width: calc((100% - 2.5rem) / 2);
  }
}

@media (max-width: 768px) {
  .project-card {
    width: 100%;
  }
}

.project-card:hover {
  transform: translateY(-12px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6), 0 0 20px rgba(255, 107, 61, 0.2);
  border-color: rgba(255, 107, 61, 0.3);
}

.project-image {
  position: relative;
  height: 220px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(18, 11, 13, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.btn-link {
  background: var(--accent-primary);
  color: white;
  padding: 0.8rem 1.5rem;
  border-radius: 50px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transform: translateY(20px);
  transition: all 0.3s ease;
}

.project-card:hover .btn-link {
  transform: translateY(0);
}

.btn-link:hover {
  background: #ff521c;
  box-shadow: 0 4px 15px rgba(255, 107, 61, 0.4);
}

.btn-demo {
  background: transparent;
  border: 1px solid var(--accent-primary);
}

.btn-demo:hover {
  background: rgba(255, 107, 61, 0.1);
  box-shadow: none;
}

.project-content {
  padding: 2rem;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}

.project-content h3 {
  font-size: 1.4rem;
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.project-content p {
  color: var(--text-secondary);
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  flex-grow: 1;
}

.project-techs {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.project-techs span {
  background: rgba(255, 107, 61, 0.1);
  color: var(--accent-primary);
  padding: 0.3rem 0.8rem;
  border-radius: 50px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(255, 107, 61, 0.2);
}
</style>
