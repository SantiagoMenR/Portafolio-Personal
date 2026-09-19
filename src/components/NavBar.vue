<template>
  <header :class="{ 'scrolled': isScrolled }" class="navbar">
    <nav class="container nav-content">
      <div class="nav-brand">
        <a href="#about" @click.prevent="scrollTo('#about')">
          <span>Santiago</span><span class="brand-accent">Mendoza</span>
        </a>
      </div>
      
      <div class="nav-menu" :class="{ 'active': isMenuOpen }">
        <a v-for="link in links" 
           :key="link.id" 
           :href="link.id"
           :class="{ 'active': currentSection === link.id.substring(1) }"
           @click.prevent="scrollTo(link.id)">
          {{ link.name }}
        </a>
      </div>
      
      <div class="hamburger" :class="{ 'active': isMenuOpen }" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isScrolled = ref(false);
const isMenuOpen = ref(false);
const currentSection = ref('about');

const links = [
  { name: 'About Me', id: '#about' },
  { name: 'Techs', id: '#techs' },
  { name: 'Projects', id: '#projects' },
  { name: 'Formación', id: '#formacion' },
  { name: 'Contacto', id: '#contacto' }
];

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const scrollTo = (id) => {
  isMenuOpen.value = false;
  const element = document.querySelector(id);
  if (element) {
    window.scrollTo({
      top: element.offsetTop - 80,
      behavior: 'smooth'
    });
  }
};

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
  
  // Update active section
  const sections = links.map(link => document.querySelector(link.id)).filter(Boolean);
  let current = '';
  
  sections.forEach(section => {
    const sectionTop = section.offsetTop;
    if (window.scrollY >= sectionTop - 200) {
      current = section.getAttribute('id');
    }
  });
  
  if (current) {
    currentSection.value = current;
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 1.5rem 0;
  transition: all 0.3s ease;
  background: transparent;
}

.navbar.scrolled {
  background: rgba(18, 11, 13, 0.85);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 1rem 0;
  border-bottom: 1px solid var(--glass-border);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
}

.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand a {
  font-size: 1.5rem;
  font-weight: 700;
  font-family: var(--font-heading);
  display: flex;
  gap: 0.3rem;
}

.brand-accent {
  color: var(--accent-primary);
}

.nav-menu {
  display: flex;
  gap: 2rem;
}

.nav-menu a {
  font-size: 1rem;
  font-weight: 500;
  color: var(--text-secondary);
  transition: all 0.3s ease;
  position: relative;
  padding: 0.5rem 0;
}

.nav-menu a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--accent-primary);
  transition: width 0.3s ease;
}

.nav-menu a:hover,
.nav-menu a.active {
  color: var(--text-primary);
}

.nav-menu a:hover::after,
.nav-menu a.active::after {
  width: 100%;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
  gap: 5px;
  z-index: 1001;
}

.hamburger span {
  width: 25px;
  height: 2px;
  background-color: var(--text-primary);
  transition: all 0.3s ease;
}

@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }
  
  .hamburger.active span:nth-child(1) {
    transform: translateY(7px) rotate(45deg);
  }
  
  .hamburger.active span:nth-child(2) {
    opacity: 0;
  }
  
  .hamburger.active span:nth-child(3) {
    transform: translateY(-7px) rotate(-45deg);
  }

  .nav-menu {
    position: fixed;
    top: 0;
    right: -100%;
    width: 70%;
    height: 100vh;
    background: var(--bg-secondary);
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 3rem;
    transition: right 0.4s cubic-bezier(0.77, 0, 0.175, 1);
    box-shadow: -10px 0 30px rgba(0, 0, 0, 0.5);
  }

  .nav-menu.active {
    right: 0;
  }
  
  .nav-menu a {
    font-size: 1.5rem;
  }
}
</style>
