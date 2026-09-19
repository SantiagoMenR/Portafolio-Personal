<template>
  <section id="about" class="section hero-section">
    <div class="container">
      <div class="hero-content">
        <div class="hero-text">
          <h2 class="greeting">¡Hola! Soy</h2>
          <h1 class="name">Santiago <span class="gradient-text">Mendoza Rivera</span></h1>
          <h3 class="role">Desarrollador Full Stack</h3>
          
          <p class="bio">
            Un apasionado desarrollador full stack con experiencia en la creación de aplicaciones web modernas y escalables. Me especializo en tecnologías frontend y backend, siempre buscando las mejores prácticas y soluciones innovadoras.
          </p>
          <p class="bio">
            Mi enfoque se centra en escribir código limpio, mantenible y eficiente, con una fuerte atención a la experiencia del usuario y la accesibilidad. Disfruto trabajando en equipo y aprendiendo nuevas tecnologías constantemente.
          </p>
          
          <div class="stats-container">
            <div class="stat-box glass-panel" v-for="(stat, index) in stats" :key="index" ref="statBoxes">
              <span class="stat-number">{{ stat.number }}</span>
              <span class="stat-label">{{ stat.label }}</span>
            </div>
          </div>
          
          <div class="hero-actions">
            <a href="#projects" class="btn btn-primary" @click.prevent="scrollTo('#projects')">Ver Proyectos</a>
            <a href="#contacto" class="btn btn-secondary" @click.prevent="scrollTo('#contacto')">Contactarme</a>
          </div>
        </div>
        
        <div class="hero-image-wrapper" ref="imageWrapper">
          <div class="profile-frame glass-panel">
            <!-- Placeholder hasta que se añadan las reales en src/assets/ -->
            <img src="../assets/Foto-nueva.jpeg" alt="Santiago Mendoza" class="profile-img">
            
            <div class="floating-badge badge-1 glass-panel">
              <i class="fa-brands fa-vuejs"></i>
            </div>
            <div class="floating-badge badge-2 glass-panel">
              <i class="fa-brands fa-python"></i>
            </div>
            <div class="floating-badge badge-3 glass-panel">
              <i class="fa-brands fa-java"></i>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import gsap from 'gsap';

const statBoxes = ref([]);
const imageWrapper = ref(null);

const stats = [
  { number: '1+', label: 'Años de Experiencia' },
  { number: '10+', label: 'Proyectos Completados' },
  { number: '11+', label: 'Tecnologías Dominadas' }
];

const scrollTo = (id) => {
  const element = document.querySelector(id);
  if (element) {
    window.scrollTo({
      top: element.offsetTop - 80,
      behavior: 'smooth'
    });
  }
};

onMounted(() => {
  // GSAP Entrance Animations
  const tl = gsap.timeline({ defaults: { ease: 'power3.out' } });
  
  tl.fromTo('.greeting', { y: 30, opacity: 0 }, { y: 0, opacity: 1, duration: 0.8, delay: 0.2 })
    .fromTo('.name', { y: 30, opacity: 0 }, { y: 0, opacity: 1, duration: 0.8 }, '-=0.6')
    .fromTo('.role', { y: 30, opacity: 0 }, { y: 0, opacity: 1, duration: 0.8 }, '-=0.6')
    .fromTo('.bio', { y: 30, opacity: 0 }, { y: 0, opacity: 1, duration: 0.8, stagger: 0.2 }, '-=0.6')
    .fromTo('.hero-actions', { y: 30, opacity: 0 }, { y: 0, opacity: 1, duration: 0.8 }, '-=0.4')
    .fromTo(statBoxes.value, { y: 30, opacity: 0 }, { y: 0, opacity: 1, duration: 0.8, stagger: 0.15 }, '-=0.6')
    .fromTo(imageWrapper.value, { x: 50, opacity: 0 }, { x: 0, opacity: 1, duration: 1 }, '-=1')
    .fromTo('.floating-badge', { scale: 0, opacity: 0 }, { scale: 1, opacity: 1, duration: 0.6, stagger: 0.2, ease: 'back.out(1.7)' }, '-=0.5');
    
  // Floating animation for badges
  gsap.to('.badge-1', { y: -15, duration: 2, repeat: -1, yoyo: true, ease: 'sine.inOut' });
  gsap.to('.badge-2', { y: -10, duration: 2.5, repeat: -1, yoyo: true, ease: 'sine.inOut', delay: 0.5 });
  gsap.to('.badge-3', { y: -20, duration: 2.2, repeat: -1, yoyo: true, ease: 'sine.inOut', delay: 1 });
});
</script>

<style scoped>
.hero-section {
  padding-top: 120px;
  position: relative;
  overflow: hidden;
}

/* Decoración de fondo */
.hero-section::before {
  content: '';
  position: absolute;
  top: 10%;
  right: -10%;
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(255,107,61,0.15) 0%, rgba(18,11,13,0) 70%);
  border-radius: 50%;
  z-index: 0;
}

.hero-section::after {
  content: '';
  position: absolute;
  bottom: -10%;
  left: -10%;
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, rgba(122,31,31,0.2) 0%, rgba(18,11,13,0) 70%);
  border-radius: 50%;
  z-index: 0;
}

.container {
  position: relative;
  z-index: 1;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.greeting {
  font-size: 1.5rem;
  color: var(--accent-primary);
  margin-bottom: 0.5rem;
  font-family: var(--font-body);
}

.name {
  font-size: 4rem;
  line-height: 1.1;
  margin-bottom: 0.5rem;
}

.role {
  font-size: 2rem;
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
  font-weight: 400;
}

.bio {
  font-size: 1.1rem;
  color: var(--text-secondary);
  margin-bottom: 1rem;
}

.stats-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin: 2.5rem 0;
}

.stat-box {
  padding: 1.5rem 1rem;
  text-align: center;
  transition: transform 0.3s ease, border-color 0.3s ease;
}

.stat-box:hover {
  transform: translateY(-5px);
  border-color: rgba(255, 107, 61, 0.3);
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--accent-primary);
  font-family: var(--font-heading);
}

.stat-label {
  font-size: 0.85rem;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.hero-actions {
  display: flex;
  gap: 1rem;
}

.btn {
  padding: 0.8rem 2rem;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1rem;
  transition: all 0.3s ease;
  cursor: pointer;
}

.btn-primary {
  background: var(--accent-primary);
  color: white;
  box-shadow: 0 4px 15px rgba(255, 107, 61, 0.3);
}

.btn-primary:hover {
  background: #ff521c;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255, 107, 61, 0.4);
}

.btn-secondary {
  background: transparent;
  color: var(--text-primary);
  border: 1px solid var(--glass-border);
}

.btn-secondary:hover {
  background: var(--bg-tertiary);
  border-color: var(--text-primary);
}

/* Image styling */
.hero-image-wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.profile-frame {
  position: relative;
  width: 100%;
  max-width: 400px;
  aspect-ratio: 6/7;
  border-radius: 24px;
  padding: 1rem;
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 16px;
  filter: grayscale(20%) contrast(1.1);
  transition: filter 0.5s ease;
}

.profile-frame:hover .profile-img {
  filter: grayscale(0%) contrast(1);
}

.floating-badge {
  position: absolute;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.8rem;
  color: var(--accent-primary);
  box-shadow: 0 10px 25px rgba(0,0,0,0.5);
  border: 1px solid rgba(255,255,255,0.1);
}

.badge-1 {
  top: 10%;
  left: -20px;
}

.badge-2 {
  bottom: 20%;
  right: -20px;
  font-size: 2rem;
}

.badge-3 {
  top: -10px;
  right: 15%;
}

@media (max-width: 992px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 3rem;
  }
  
  .hero-text {
    order: 2;
  }
  
  .hero-image-wrapper {
    order: 1;
  }
  
  .hero-actions {
    justify-content: center;
  }
}

@media (max-width: 768px) {
  .name {
    font-size: 3rem;
  }
  
  .role {
    font-size: 1.5rem;
  }
  
  .stats-container {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
</style>
