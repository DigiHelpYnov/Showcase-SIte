<template>
  <div>
    <NuxtRouteAnnouncer />
    
    <!-- Page de bienvenue avec animations -->
    <div class="welcome-container">
      <!-- Animation de chargement -->
      <div v-if="isLoading" class="loading-screen">
        <div class="loading-spinner">
          <div class="spinner-ring"></div>
          <div class="spinner-ring"></div>
          <div class="spinner-ring"></div>
        </div>
        <div class="loading-text">
          <span class="loading-dots">Chargement</span>
        </div>
      </div>

      <!-- Contenu principal -->
      <div v-else class="welcome-content">
        <!-- Header avec animation d'apparition -->
        <header class="welcome-header">
          <div class="logo-container">
            <div class="logo-circle">
              <span class="logo-text">V</span>
            </div>
          </div>
          <h1 class="welcome-title">
            <span class="title-line">Bienvenue sur</span>
            <span class="title-line highlight">Vitrine</span>
          </h1>
          <p class="welcome-subtitle">
            Votre plateforme moderne et élégante
          </p>
        </header>

        <!-- Section principale avec cartes animées -->
        <main class="welcome-main">
          <div class="features-grid">
            <div class="feature-card" v-for="(feature, index) in features" :key="index" :style="{ animationDelay: `${index * 0.2}s` }">
              <div class="feature-icon">
                <i :class="feature.icon"></i>
              </div>
              <h3 class="feature-title">{{ feature.title }}</h3>
              <p class="feature-description">{{ feature.description }}</p>
            </div>
          </div>
        </main>

        <!-- Boutons d'action -->
        <footer class="welcome-footer">
          <button class="cta-button primary" @click="startJourney">
            <span>Commencer</span>
            <div class="button-ripple"></div>
          </button>
          <button class="cta-button secondary" @click="learnMore">
            <span>En savoir plus</span>
          </button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// État de chargement
const isLoading = ref(true)

// Fonctionnalités à afficher
const features = ref([
  {
    icon: 'fas fa-rocket',
    title: 'Performance',
    description: 'Rapide et optimisé pour une expérience fluide'
  },
  {
    icon: 'fas fa-palette',
    title: 'Design moderne',
    description: 'Interface élégante et intuitive'
  },
  {
    icon: 'fas fa-mobile-alt',
    title: 'Responsive',
    description: 'Parfaitement adapté à tous les écrans'
  },
  {
    icon: 'fas fa-shield-alt',
    title: 'Sécurisé',
    description: 'Protection et confidentialité garanties'
  }
])

// Simulation du chargement
onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 2500)
})

// Actions des boutons
const startJourney = () => {
  console.log('Démarrage du parcours utilisateur')
  // Ici vous pouvez ajouter la logique de navigation
}

const learnMore = () => {
  console.log('En savoir plus')
  // Ici vous pouvez ajouter la logique pour plus d'informations
}
</script>

<style scoped>
/* Variables CSS pour la cohérence */
:root {
  --primary-color: #6366f1;
  --secondary-color: #8b5cf6;
  --accent-color: #06b6d4;
  --text-primary: #1f2937;
  --text-secondary: #6b7280;
  --background: #ffffff;
  --surface: #f9fafb;
  --border: #e5e7eb;
  --shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

/* Conteneur principal */
.welcome-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  position: relative;
  overflow: hidden;
}

/* Animation de chargement */
.loading-screen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.loading-spinner {
  position: relative;
  width: 80px;
  height: 80px;
  margin-bottom: 2rem;
}

.spinner-ring {
  position: absolute;
  width: 100%;
  height: 100%;
  border: 3px solid transparent;
  border-top: 3px solid #ffffff;
  border-radius: 50%;
  animation: spin 1.5s linear infinite;
}

.spinner-ring:nth-child(2) {
  width: 60px;
  height: 60px;
  top: 10px;
  left: 10px;
  border-top-color: rgba(255, 255, 255, 0.7);
  animation-duration: 1.2s;
  animation-direction: reverse;
}

.spinner-ring:nth-child(3) {
  width: 40px;
  height: 40px;
  top: 20px;
  left: 20px;
  border-top-color: rgba(255, 255, 255, 0.5);
  animation-duration: 0.8s;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loading-text {
  color: white;
  font-size: 1.2rem;
  font-weight: 500;
}

.loading-dots::after {
  content: '';
  animation: dots 1.5s infinite;
}

@keyframes dots {
  0%, 20% { content: ''; }
  40% { content: '.'; }
  60% { content: '..'; }
  80%, 100% { content: '...'; }
}

/* Contenu principal */
.welcome-content {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  animation: fadeInUp 0.8s ease-out;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Header */
.welcome-header {
  text-align: center;
  margin-bottom: 4rem;
}

.logo-container {
  margin-bottom: 2rem;
}

.logo-circle {
  width: 100px;
  height: 100px;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  box-shadow: var(--shadow-lg);
  animation: pulse 2s infinite;
}

.logo-text {
  font-size: 2.5rem;
  font-weight: bold;
  color: white;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.welcome-title {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.title-line {
  display: block;
  color: white;
  animation: slideInLeft 0.8s ease-out;
}

.title-line:nth-child(2) {
  animation-delay: 0.2s;
}

.highlight {
  background: linear-gradient(135deg, #fbbf24, #f59e0b);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.welcome-subtitle {
  font-size: 1.3rem;
  color: rgba(255, 255, 255, 0.8);
  font-weight: 300;
  animation: fadeIn 1s ease-out 0.4s both;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* Grille des fonctionnalités */
.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  max-width: 1000px;
  width: 100%;
  margin-bottom: 4rem;
}

.feature-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s ease;
  animation: slideInUp 0.6s ease-out both;
}

.feature-card:hover {
  transform: translateY(-10px);
  background: rgba(255, 255, 255, 0.2);
  box-shadow: var(--shadow-lg);
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.feature-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, var(--accent-color), var(--primary-color));
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  font-size: 1.5rem;
  color: white;
}

.feature-title {
  font-size: 1.3rem;
  font-weight: 600;
  color: white;
  margin-bottom: 1rem;
}

.feature-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
}

/* Footer avec boutons */
.welcome-footer {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
  justify-content: center;
}

.cta-button {
  position: relative;
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  overflow: hidden;
  min-width: 150px;
}

.cta-button.primary {
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: white;
  box-shadow: var(--shadow);
}

.cta-button.primary:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.cta-button.secondary {
  background: transparent;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.cta-button.secondary:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.5);
}

.button-ripple {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: width 0.6s, height 0.6s;
}

.cta-button:active .button-ripple {
  width: 300px;
  height: 300px;
}

/* Responsive */
@media (max-width: 768px) {
  .welcome-title {
    font-size: 2.5rem;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .welcome-footer {
    flex-direction: column;
    align-items: center;
  }
  
  .cta-button {
    width: 100%;
    max-width: 300px;
  }
}

@media (max-width: 480px) {
  .welcome-content {
    padding: 1rem;
  }
  
  .welcome-title {
    font-size: 2rem;
  }
  
  .logo-circle {
    width: 80px;
    height: 80px;
  }
  
  .logo-text {
    font-size: 2rem;
  }
}
</style>
