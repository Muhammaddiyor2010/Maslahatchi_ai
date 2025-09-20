<template>
  <nav class="fixed top-0 w-full z-50 glass">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center py-4">
        <div class="flex items-center space-x-2">
          <i class="fas fa-robot text-2xl text-primary"></i>
          <span class="text-xl font-bold gradient-text">Maslahatchi AI</span>
        </div>
        <div class="hidden md:flex items-center space-x-8">
          <router-link 
            to="/" 
            class="hover:text-primary transition-colors"
            :class="{ 'text-primary': $route.path === '/' }"
          >
            Bosh sahifa
          </router-link>
          <router-link 
            to="/features" 
            class="hover:text-primary transition-colors"
            :class="{ 'text-primary': $route.path === '/features' }"
          >
            Xususiyatlar
          </router-link>
          <router-link 
            to="/pricing" 
            class="hover:text-primary transition-colors"
            :class="{ 'text-primary': $route.path === '/pricing' }"
          >
            Narxlar
          </router-link>
          <router-link 
            to="/about" 
            class="hover:text-primary transition-colors"
            :class="{ 'text-primary': $route.path === '/about' }"
          >
            Biz haqimizda
          </router-link>
          <router-link 
            to="/contact" 
            class="hover:text-primary transition-colors"
            :class="{ 'text-primary': $route.path === '/contact' }"
          >
            Aloqa
          </router-link>
          <button @click="$emit('toggle-theme')" class="p-2 rounded-lg hover:bg-white/10 transition-colors theme-toggle">
            <i :class="isDark ? 'fas fa-sun text-yellow-400' : 'fas fa-moon text-blue-400'"></i>
          </button>
        </div>
        <button @click="toggleMobileMenu" class="md:hidden">
          <i class="fas fa-bars text-xl"></i>
        </button>
      </div>
    </div>
    
    <!-- Mobile Menu -->
    <div v-show="showMobileMenu" class="md:hidden glass border-t border-white/20">
      <div class="px-4 py-4 space-y-4">
        <router-link 
          to="/" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors"
        >
          Bosh sahifa
        </router-link>
        <router-link 
          to="/features" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors"
        >
          Xususiyatlar
        </router-link>
        <router-link 
          to="/pricing" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors"
        >
          Narxlar
        </router-link>
        <router-link 
          to="/about" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors"
        >
          Biz haqimizda
        </router-link>
        <router-link 
          to="/contact" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors"
        >
          Aloqa
        </router-link>
        <div class="pt-4 border-t border-white/20">
          <button @click="$emit('toggle-theme'); toggleMobileMenu()" class="flex items-center space-x-2 hover:text-primary transition-colors">
            <i :class="isDark ? 'fas fa-sun text-yellow-400' : 'fas fa-moon text-blue-400'"></i>
            <span>{{ isDark ? 'Light Mode' : 'Dark Mode' }}</span>
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navigation',
  props: {
    isDark: {
      type: Boolean,
      default: true
    }
  },
  emits: ['toggle-theme'],
  data() {
    return {
      showMobileMenu: false
    }
  },
  methods: {
    toggleMobileMenu() {
      this.showMobileMenu = !this.showMobileMenu;
    }
  }
}
</script>

<style scoped>
.text-primary {
  color: #6366f1;
}
</style>