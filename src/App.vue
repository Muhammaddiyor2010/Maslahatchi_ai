<template>
  <div id="app" :class="themeClasses">
    <!-- Navigation -->
    <Navigation @toggle-theme="toggleTheme" :is-dark="isDark" />
    
    <!-- Router View -->
    <router-view></router-view>
    
    <!-- Footer -->
    <Footer />
    
    <!-- Welcome Modal -->
    <WelcomeModal 
      :show="showWelcomeModal" 
      @close="closeWelcomeModal" 
    />
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue'
import Footer from './components/Footer.vue'
import WelcomeModal from './components/WelcomeModal.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    Footer,
    WelcomeModal
  },
  data() {
    return {
      isDark: true,
      showWelcomeModal: false
    }
  },
  computed: {
    themeClasses() {
      return this.isDark 
        ? 'bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 min-h-screen text-white dark'
        : 'bg-gradient-to-br from-blue-50 via-white to-purple-50 min-h-screen text-gray-900 light'
    }
  },
  methods: {
    toggleTheme() {
      this.isDark = !this.isDark
      localStorage.setItem('theme', this.isDark ? 'dark' : 'light')
      document.documentElement.classList.toggle('dark', this.isDark)
    },
    
    closeWelcomeModal() {
      this.showWelcomeModal = false
    },
    
    checkWelcomeModal() {
      // Check if user has seen the welcome modal before
      const hasSeenWelcome = localStorage.getItem('welcomeModalSeen')
      if (!hasSeenWelcome) {
        // Show modal after a short delay to let the page load
        setTimeout(() => {
          this.showWelcomeModal = true
        }, 1000)
      }
    }
  },
  mounted() {
    // Load theme from localStorage
    const savedTheme = localStorage.getItem('theme')
    if (savedTheme) {
      this.isDark = savedTheme === 'dark'
    } else {
      // Check system preference
      this.isDark = window.matchMedia('(prefers-color-scheme: dark)').matches
    }
    document.documentElement.classList.toggle('dark', this.isDark)
    
    // Check if welcome modal should be shown
    this.checkWelcomeModal()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');

body { 
  font-family: 'Inter', sans-serif; 
  margin: 0;
  padding: 0;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.gradient-text { 
  background: linear-gradient(45deg, #6366f1, #8b5cf6); 
  background-clip: text;
  -webkit-background-clip: text; 
  -webkit-text-fill-color: transparent; 
}

/* Dark mode glass effect */
.dark .glass { 
  backdrop-filter: blur(16px); 
  background: rgba(255, 255, 255, 0.1); 
  border: 1px solid rgba(255, 255, 255, 0.2); 
}

/* Light mode glass effect */
.light .glass { 
  backdrop-filter: blur(16px); 
  background: rgba(255, 255, 255, 0.9); 
  border: 1px solid rgba(255, 255, 255, 0.2); 
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12), 0 2px 8px rgba(0, 0, 0, 0.08);
}

.animate-float { 
  animation: float 6s ease-in-out infinite; 
}

@keyframes float { 
  0%, 100% { transform: translateY(0px); } 
  50% { transform: translateY(-20px); } 
}

.animate-glow { 
  animation: glow 2s ease-in-out infinite alternate; 
}

@keyframes glow { 
  from { box-shadow: 0 0 20px rgba(99, 102, 241, 0.3); } 
  to { box-shadow: 0 0 30px rgba(99, 102, 241, 0.6); } 
}

/* Theme transition */
#app {
  transition: all 0.3s ease;
}

/* Light mode specific styles */
.light .text-gray-300 {
  color: #4b5563;
}

.light .text-gray-400 {
  color: #6b7280;
}

.light .text-white {
  color: #1f2937;
}

.light .bg-gray-800 {
  background-color: #f8fafc;
  color: #1f2937;
}

.light .bg-gray-700 {
  background-color: #e2e8f0;
  color: #1f2937;
}

.light .bg-gray-600 {
  background-color: #cbd5e1;
}

.light .border-gray-600 {
  border-color: #cbd5e1;
}

.light .border-white\/10 {
  border-color: rgba(0, 0, 0, 0.1);
}

.light .border-white\/20 {
  border-color: rgba(0, 0, 0, 0.15);
}

/* Light mode navigation */
.light nav.glass {
  background: rgba(255, 255, 255, 0.95);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

/* Light mode footer */
.light footer {
  background: rgba(255, 255, 255, 0.9);
  border-top: 1px solid rgba(0, 0, 0, 0.1);
}

/* Light mode button hover effects */
.light .hover\:bg-white\/10:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

.light .hover\:bg-primary\/10:hover {
  background-color: rgba(99, 102, 241, 0.1);
}

/* Light mode form inputs */
.light input, .light textarea {
  background-color: #ffffff;
  border-color: #d1d5db;
  color: #1f2937;
}

.light input:focus, .light textarea:focus {
  border-color: #6366f1;
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

/* Dark mode specific styles */
.dark .text-gray-900 {
  color: #f9fafb;
}

/* Theme toggle button animation */
.theme-toggle {
  transition: transform 0.2s ease;
}

.theme-toggle:hover {
  transform: scale(1.1);
}

/* Slide animations */
.animate-slide-in-left {
  animation: slideInLeft 0.8s ease-out;
}

.animate-slide-in-right {
  animation: slideInRight 0.8s ease-out;
}

.animate-slide-in-up {
  animation: slideInUp 0.8s ease-out;
}

.animate-slide-in-down {
  animation: slideInDown 0.8s ease-out;
}

.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out;
}

.animate-fade-in-down {
  animation: fadeInDown 0.8s ease-out;
}

.animate-fade-in-left {
  animation: fadeInLeft 0.8s ease-out;
}

.animate-fade-in-right {
  animation: fadeInRight 0.8s ease-out;
}

/* Keyframes */
@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-100px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(100px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(100px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideInDown {
  from {
    opacity: 0;
    transform: translateY(-100px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
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

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Staggered animations */
.animate-delay-100 {
  animation-delay: 0.1s;
}

.animate-delay-200 {
  animation-delay: 0.2s;
}

.animate-delay-300 {
  animation-delay: 0.3s;
}

.animate-delay-400 {
  animation-delay: 0.4s;
}

.animate-delay-500 {
  animation-delay: 0.5s;
}

.animate-delay-600 {
  animation-delay: 0.6s;
}

.animate-delay-700 {
  animation-delay: 0.7s;
}

.animate-delay-800 {
  animation-delay: 0.8s;
}

.animate-delay-900 {
  animation-delay: 0.9s;
}

.animate-delay-1000 {
  animation-delay: 1.0s;
}

.animate-delay-1100 {
  animation-delay: 1.1s;
}

.animate-delay-1200 {
  animation-delay: 1.2s;
}

.animate-delay-1300 {
  animation-delay: 1.3s;
}

.animate-delay-1400 {
  animation-delay: 1.4s;
}

.animate-delay-1500 {
  animation-delay: 1.5s;
}
</style>
