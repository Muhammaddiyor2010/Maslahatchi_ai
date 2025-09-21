<template>
  <nav class="fixed top-0 w-full z-50 glass animate-slide-in-down">
    <div class="max-w-7xl mx-auto px-3 sm:px-4 lg:px-8">
      <div class="flex justify-between items-center py-3 sm:py-4">
        <div class="flex items-center space-x-1 sm:space-x-2 animate-fade-in-left">
          <i class="fas fa-robot text-lg sm:text-xl md:text-2xl text-primary"></i>
          <span class="text-lg sm:text-xl font-bold gradient-text">Maslahatchi AI</span>
        </div>
        <div class="hidden lg:flex items-center space-x-6 xl:space-x-8 animate-fade-in-right">
          <router-link 
            to="/" 
            class="hover:text-primary transition-colors text-sm xl:text-base animate-fade-in-up animate-delay-100"
            :class="{ 'text-primary': $route.path === '/' }"
          >
            Bosh sahifa
          </router-link>
          <router-link 
            to="/features" 
            class="hover:text-primary transition-colors text-sm xl:text-base animate-fade-in-up animate-delay-200"
            :class="{ 'text-primary': $route.path === '/features' }"
          >
            Xususiyatlar
          </router-link>
          <router-link 
            to="/advice" 
            class="hover:text-primary transition-colors text-sm xl:text-base animate-fade-in-up animate-delay-300"
            :class="{ 'text-primary': $route.path === '/advice' }"
          >
            Maslahatlar
          </router-link>
          <router-link 
            to="/chat" 
            class="hover:text-primary transition-colors text-sm xl:text-base animate-fade-in-up animate-delay-400"
            :class="{ 'text-primary': $route.path === '/chat' }"
          >
            AI Chat
          </router-link>
          <router-link 
            to="/pricing" 
            class="hover:text-primary transition-colors text-sm xl:text-base animate-fade-in-up animate-delay-500"
            :class="{ 'text-primary': $route.path === '/pricing' }"
          >
            Narxlar
          </router-link>
          <router-link 
            to="/about" 
            class="hover:text-primary transition-colors text-sm xl:text-base animate-fade-in-up animate-delay-600"
            :class="{ 'text-primary': $route.path === '/about' || $route.path === '/contact' }"
          >
            Biz haqimizda & Aloqa
          </router-link>
          <button @click="$emit('toggle-theme')" class="p-2 rounded-lg hover:bg-white/10 transition-colors theme-toggle animate-fade-in-up animate-delay-700">
            <i :class="isDark ? 'fas fa-sun text-yellow-400' : 'fas fa-moon text-blue-400'"></i>
          </button>
        </div>
        <button @click="toggleMobileMenu" class="lg:hidden p-2 animate-fade-in-right">
          <i class="fas fa-bars text-lg sm:text-xl"></i>
        </button>
      </div>
    </div>
    
    <!-- Mobile Menu -->
    <div v-show="showMobileMenu" class="lg:hidden glass border-t border-white/20 animate-slide-in-down">
      <div class="px-3 sm:px-4 py-3 sm:py-4 space-y-3 sm:space-y-4">
        <router-link 
          to="/" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors text-sm sm:text-base py-1"
        >
          Bosh sahifa
        </router-link>
        <router-link 
          to="/features" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors text-sm sm:text-base py-1"
        >
          Xususiyatlar
        </router-link>
        <router-link 
          to="/advice" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors text-sm sm:text-base py-1"
        >
          Maslahatlar
        </router-link>
        <router-link 
          to="/chat" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors text-sm sm:text-base py-1"
        >
          AI Chat
        </router-link>
        <router-link 
          to="/pricing" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors text-sm sm:text-base py-1"
        >
          Narxlar
        </router-link>
        <router-link 
          to="/about" 
          @click="toggleMobileMenu" 
          class="block hover:text-primary transition-colors text-sm sm:text-base py-1"
        >
          Biz haqimizda & Aloqa
        </router-link>
        <div class="pt-3 sm:pt-4 border-t border-white/20">
          <button @click="$emit('toggle-theme'); toggleMobileMenu()" class="flex items-center space-x-2 hover:text-primary transition-colors text-sm sm:text-base py-1">
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