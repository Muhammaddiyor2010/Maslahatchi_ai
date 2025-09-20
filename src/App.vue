<template>
  <div id="app" :class="themeClasses">
    <!-- Navigation -->
    <Navigation @toggle-theme="toggleTheme" :is-dark="isDark" />
    
    <!-- Router View -->
    <router-view></router-view>
    
    <!-- Footer -->
    <Footer />
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    Footer
  },
  data() {
    return {
      isDark: true
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
</style>
