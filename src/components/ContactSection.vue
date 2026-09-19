<template>
  <section id="contacto" class="section contact-section">
    <div class="container">
      <h2 class="section-title">Contacto</h2>
      
      <div class="contact-content">
        <div class="contact-info">
          <h3>¡Trabajemos Juntos!</h3>
          <p>
            ¿Tienes un proyecto en mente? Me encantaría escuchar sobre él. Estoy siempre abierto a nuevas oportunidades y colaboraciones interesantes.
          </p>
          
          <div class="contact-methods">
            <a href="mailto:smrivera135@gmail.com" class="contact-method glass-panel">
              <div class="method-icon"><i class="fa-solid fa-envelope"></i></div>
              <div class="method-text">
                <h4>Email</h4>
                <span>smrivera135@gmail.com</span>
              </div>
            </a>
            
            <a href="https://github.com/SantiagoMenR" target="_blank" class="contact-method glass-panel">
              <div class="method-icon"><i class="fa-brands fa-github"></i></div>
              <div class="method-text">
                <h4>GitHub</h4>
                <span>github.com/SantiagoMenR</span>
              </div>
            </a>
          </div>
        </div>
        
        <div class="contact-action glass-panel">
          <div class="action-card whatsapp-card">
            <i class="fa-brands fa-whatsapp action-bg-icon"></i>
            <h3>¡Hablemos por WhatsApp!</h3>
            <p>Contáctame de forma rápida y directa.</p>
            <a href="https://wa.me/573106076348?text=Hola%20Santiago,%20vi%20tu%20portafolio%20y%20me%20gustaría%20hablar%20contigo%20sobre%20un%20proyecto." 
               target="_blank" class="btn-whatsapp">
              <i class="fa-brands fa-whatsapp"></i> Chatear por WhatsApp
            </a>
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

onMounted(() => {
  // Title Animation
  gsap.fromTo('.contact-section .section-title', 
    { y: 50, opacity: 0 },
    { 
      y: 0, 
      opacity: 1, 
      duration: 0.8,
      scrollTrigger: {
        trigger: '.contact-section',
        start: 'top 80%',
      }
    }
  );

  // Content Animation
  gsap.fromTo('.contact-info',
    { x: -50, opacity: 0 },
    {
      x: 0,
      opacity: 1,
      duration: 0.8,
      scrollTrigger: {
        trigger: '.contact-content',
        start: 'top 80%',
      }
    }
  );

  gsap.fromTo('.contact-action',
    { x: 50, opacity: 0 },
    {
      x: 0,
      opacity: 1,
      duration: 0.8,
      delay: 0.2,
      scrollTrigger: {
        trigger: '.contact-content',
        start: 'top 80%',
      }
    }
  );
  
  // Floating animation for the background icon
  gsap.to('.action-bg-icon', {
    y: -15,
    rotation: 5,
    duration: 3,
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  });
});
</script>

<style scoped>
.contact-section {
  background: linear-gradient(135deg, var(--bg-primary) 0%, rgba(122, 31, 31, 0.1) 100%);
  position: relative;
  overflow: hidden;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.contact-info h3 {
  font-size: 2rem;
  color: var(--accent-primary);
  margin-bottom: 1.5rem;
}

.contact-info p {
  font-size: 1.1rem;
  color: var(--text-secondary);
  line-height: 1.8;
  margin-bottom: 2.5rem;
}

.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 1.5rem;
  transition: transform 0.3s ease, border-color 0.3s ease;
  background: rgba(255, 255, 255, 0.03);
}

.contact-method:hover {
  transform: translateX(10px);
  border-color: rgba(255, 107, 61, 0.4);
}

.method-icon {
  width: 50px;
  height: 50px;
  border-radius: 12px;
  background: rgba(255, 107, 61, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  color: var(--accent-primary);
}

.method-text h4 {
  font-size: 1.1rem;
  margin-bottom: 0.2rem;
  color: var(--text-primary);
}

.method-text span {
  color: var(--text-secondary);
  font-size: 0.95rem;
}

.contact-action {
  padding: 3rem;
  position: relative;
  overflow: hidden;
  text-align: center;
  background: rgba(37, 211, 102, 0.05); /* Ligeramente verdoso por WhatsApp */
  border: 1px solid rgba(37, 211, 102, 0.1);
}

.action-bg-icon {
  position: absolute;
  top: -20px;
  right: -20px;
  font-size: 15rem;
  color: rgba(37, 211, 102, 0.05);
  z-index: 0;
}

.action-card {
  position: relative;
  z-index: 1;
}

.action-card h3 {
  font-size: 1.8rem;
  color: white;
  margin-bottom: 1rem;
}

.action-card p {
  color: var(--text-secondary);
  margin-bottom: 2.5rem;
  font-size: 1.1rem;
}

.btn-whatsapp {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  padding: 1.2rem 2.5rem;
  background: #25d366;
  color: white;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1.1rem;
  transition: all 0.3s ease;
  box-shadow: 0 10px 20px rgba(37, 211, 102, 0.3);
}

.btn-whatsapp:hover {
  background: #128c7e;
  transform: translateY(-5px);
  box-shadow: 0 15px 25px rgba(37, 211, 102, 0.4);
}

.btn-whatsapp i {
  font-size: 1.4rem;
}

@media (max-width: 992px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}
</style>
