<template>
  <section id="formacion" class="section education-section">
    <div class="container">
      <h2 class="section-title">Formación Académica</h2>
      
      <div class="timeline-container">
        <div class="timeline-line"></div>
        
        <div class="timeline-item" v-for="(item, index) in education" :key="index">
          <div class="timeline-dot"></div>
          <div class="timeline-content glass-panel">
            <div class="timeline-year">{{ item.year }}</div>
            <h3>{{ item.title }}</h3>
            <h4 class="institution">{{ item.institution }}</h4>
            <p v-if="item.description">{{ item.description }}</p>
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

gsap.registerPlugin(ScrollTrigger);

const education = [
  {
    year: 'En curso',
    title: 'Ingeniería de Software',
    institution: 'Uniminuto',
    description: 'Estudiante de Ingeniería de Software en curso.'
  },
  {
    year: '2025',
    title: 'Técnico en Desarrollo de Software',
    institution: 'Campuslands',
    description: 'Técnico en desarrollo de software especializado en backend.'
  },
  {
    year: '2025',
    title: 'Curso Django',
    institution: 'Platzi',
    description: 'Fundamentos y Aplicación de las tecnologías de backend.'
  }
];

onMounted(() => {
  // Title Animation
  gsap.fromTo('.education-section .section-title', 
    { y: 50, opacity: 0 },
    { 
      y: 0, 
      opacity: 1, 
      duration: 0.8,
      scrollTrigger: {
        trigger: '.education-section',
        start: 'top 80%',
      }
    }
  );

  // Timeline line animation
  gsap.fromTo('.timeline-line', 
    { height: 0 },
    { 
      height: '100%', 
      duration: 1.5,
      ease: 'power2.inOut',
      scrollTrigger: {
        trigger: '.timeline-container',
        start: 'top 70%',
        end: 'bottom 50%',
        scrub: 1
      }
    }
  );

  // Timeline items animation
  gsap.fromTo('.timeline-item', 
    { x: -50, opacity: 0 },
    { 
      x: 0, 
      opacity: 1, 
      duration: 0.6,
      stagger: 0.3,
      scrollTrigger: {
        trigger: '.timeline-container',
        start: 'top 70%',
      }
    }
  );
});
</script>

<style scoped>
.education-section {
  background-color: var(--bg-secondary);
}

.timeline-container {
  position: relative;
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem 0;
}

.timeline-line {
  position: absolute;
  left: 30px;
  top: 0;
  width: 4px;
  background: linear-gradient(to bottom, var(--accent-primary), var(--accent-secondary));
  border-radius: 2px;
  z-index: 0;
}

.timeline-item {
  position: relative;
  padding-left: 80px;
  margin-bottom: 3rem;
  z-index: 1;
}

.timeline-item:last-child {
  margin-bottom: 0;
}

.timeline-dot {
  position: absolute;
  left: 22px;
  top: 20px;
  width: 20px;
  height: 20px;
  background-color: var(--bg-primary);
  border: 4px solid var(--accent-primary);
  border-radius: 50%;
  box-shadow: 0 0 10px rgba(255, 107, 61, 0.5);
  transition: transform 0.3s ease;
}

.timeline-item:hover .timeline-dot {
  transform: scale(1.3);
  background-color: var(--accent-primary);
}

.timeline-content {
  padding: 2rem;
  position: relative;
  transition: transform 0.3s ease;
  background: rgba(255, 255, 255, 0.02);
}

.timeline-content::before {
  content: '';
  position: absolute;
  left: -15px;
  top: 20px;
  border-width: 15px 15px 15px 0;
  border-style: solid;
  border-color: transparent var(--glass-border) transparent transparent;
}

.timeline-item:hover .timeline-content {
  transform: translateX(10px);
  border-color: rgba(255, 107, 61, 0.3);
}

.timeline-year {
  display: inline-block;
  padding: 0.3rem 1rem;
  background: rgba(255, 107, 61, 0.1);
  color: var(--accent-primary);
  border-radius: 50px;
  font-weight: 700;
  font-size: 0.9rem;
  margin-bottom: 1rem;
  border: 1px solid rgba(255, 107, 61, 0.2);
}

.timeline-content h3 {
  font-size: 1.5rem;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
}

.institution {
  font-size: 1.1rem;
  color: var(--text-secondary);
  font-weight: 500;
  margin-bottom: 1rem;
}

.timeline-content p {
  color: var(--text-muted);
  line-height: 1.6;
}

@media (max-width: 768px) {
  .timeline-line {
    left: 20px;
  }
  
  .timeline-dot {
    left: 12px;
  }
  
  .timeline-item {
    padding-left: 60px;
  }
}
</style>
