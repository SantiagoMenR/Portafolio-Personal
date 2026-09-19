<template>
  <section id="techs" class="section tech-section">
    <div class="container">
      <h2 class="section-title gs-reveal">Mis Tecnologías</h2>
      
      <div class="techs-grid">
        <div class="tech-category glass-panel gs-reveal" v-for="(category, index) in techCategories" :key="index">
          <h3>{{ category.title }}</h3>
          <div class="tech-items">
            <div class="tech-item" v-for="(tech, tIndex) in category.items" :key="tIndex">
              <i :class="tech.icon"></i>
              <span>{{ tech.name }}</span>
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

gsap.registerPlugin(ScrollTrigger);

const techCategories = [
  {
    title: 'Frontend',
    items: [
      { name: 'Vue.js', icon: 'fa-brands fa-vuejs' },
      { name: 'TypeScript', icon: 'fa-solid fa-code' },
      { name: 'Tailwind CSS', icon: 'fa-solid fa-wind' }
    ]
  },
  {
    title: 'Backend',
    items: [
      { name: 'MySQL', icon: 'fa-solid fa-database' },
      { name: 'Python', icon: 'fa-brands fa-python' },
      { name: 'Django', icon: 'fa-brands fa-python' },
      { name: 'Java', icon: 'fa-brands fa-java' },
      { name: 'Spring Boot', icon: 'fa-solid fa-leaf' },
      { name: 'PostgreSQL', icon: 'fa-solid fa-database' }
    ]
  },
  {
    title: 'Herramientas',
    items: [
      { name: 'Git', icon: 'fa-brands fa-git-alt' },
      { name: 'GitHub', icon: 'fa-brands fa-github' },
      { name: 'Docker', icon: 'fa-brands fa-docker' }
    ]
  }
];

onMounted(() => {
  // Animación de título
  gsap.fromTo('.tech-section .section-title', 
    { y: 50, opacity: 0 },
    { 
      y: 0, 
      opacity: 1, 
      duration: 0.8,
      scrollTrigger: {
        trigger: '.tech-section',
        start: 'top 80%',
      }
    }
  );

  // Animación escalonada para las categorías
  gsap.fromTo('.tech-category', 
    { y: 50, opacity: 0 },
    { 
      y: 0, 
      opacity: 1, 
      duration: 0.8,
      stagger: 0.2,
      scrollTrigger: {
        trigger: '.techs-grid',
        start: 'top 85%',
      }
    }
  );

  // Animación escalonada para los items (icons)
  const categories = document.querySelectorAll('.tech-category');
  categories.forEach(category => {
    const items = category.querySelectorAll('.tech-item');
    gsap.fromTo(items, 
      { scale: 0.5, opacity: 0 },
      {
        scale: 1,
        opacity: 1,
        duration: 0.5,
        stagger: 0.1,
        ease: 'back.out(1.5)',
        scrollTrigger: {
          trigger: category,
          start: 'top 85%',
        }
      }
    );
  });
});
</script>

<style scoped>
.tech-section {
  background-color: var(--bg-secondary);
}

.techs-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.tech-category {
  padding: 2.5rem;
  transition: transform 0.3s ease, border-color 0.3s ease;
  background: rgba(255, 255, 255, 0.02);
}

.tech-category:hover {
  transform: translateY(-5px);
  border-color: rgba(255, 107, 61, 0.4);
}

.tech-category h3 {
  color: var(--accent-primary);
  margin-bottom: 2rem;
  font-size: 1.5rem;
  text-align: center;
  letter-spacing: 1px;
}

.tech-items {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.2rem;
}

.tech-item {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  transition: all 0.3s ease;
  cursor: default;
}

.tech-item:hover {
  background: var(--accent-primary);
  color: white;
  transform: scale(1.05);
  box-shadow: 0 5px 15px rgba(255, 107, 61, 0.3);
  border-color: transparent;
}

.tech-item i {
  font-size: 1.5rem;
  color: var(--accent-primary);
  transition: color 0.3s ease;
}

.tech-item:hover i {
  color: white;
}

.tech-item span {
  font-size: 0.95rem;
  font-weight: 500;
}

@media (max-width: 992px) {
  .techs-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .tech-items {
    grid-template-columns: 1fr;
  }
}
</style>
