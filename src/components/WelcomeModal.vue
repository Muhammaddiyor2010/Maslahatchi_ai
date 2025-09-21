<template>
  <div v-if="show" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50 backdrop-blur-sm p-4">
    <div class="glass rounded-xl sm:rounded-2xl p-6 sm:p-8 max-w-sm sm:max-w-md mx-auto w-full animate-fade-in">
      <div class="text-center">
        <!-- Icon -->
        <div class="mb-4 sm:mb-6">
          <i class="fas fa-hand-wave text-4xl sm:text-5xl md:text-6xl text-primary animate-bounce"></i>
        </div>
        
        <!-- Title -->
        <h2 class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4 gradient-text">
          Xush kelibsiz!
        </h2>
        
        <!-- Description -->
        <p class="text-gray-300 mb-6 sm:mb-8 text-base sm:text-lg leading-relaxed">
          Maslahatchi AI ga xush kelibsiz! 
          <br><br>
          Sizga qo'llanma kerakmi?
        </p>
        
        <!-- Buttons -->
        <div class="flex flex-col sm:flex-row gap-3 sm:gap-4 justify-center">
          <button @click="handleYes" 
                  class="bg-gradient-to-r from-primary to-secondary px-6 sm:px-8 py-2 sm:py-3 rounded-lg font-semibold hover:scale-105 transition-transform text-white text-sm sm:text-base">
            <i class="fas fa-book mr-2"></i>
            Ha, qo'llanma kerak
          </button>
          
          <button @click="handleNo" 
                  class="border-2 border-primary px-6 sm:px-8 py-2 sm:py-3 rounded-lg font-semibold hover:bg-primary/10 transition-colors text-primary text-sm sm:text-base">
            <i class="fas fa-times mr-2"></i>
            Yo'q, rahmat
          </button>
        </div>
        
        <!-- Skip text -->
        <p class="text-gray-400 text-xs sm:text-sm mt-3 sm:mt-4">
          Bu oynani keyinroq ko'rish uchun <span class="text-primary cursor-pointer hover:underline" @click="handleNo">bu yerni bosing</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WelcomeModal',
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleYes() {
      // Save that user has seen the modal
      localStorage.setItem('welcomeModalSeen', 'true');
      
      // Navigate to help page
      this.$router.push('/help');
      
      // Emit close event
      this.$emit('close');
    },
    
    handleNo() {
      // Save that user has seen the modal
      localStorage.setItem('welcomeModalSeen', 'true');
      
      // Emit close event
      this.$emit('close');
    }
  }
}
</script>

<style scoped>
.animate-fade-in {
  animation: fadeIn 0.5s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.animate-bounce {
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}
</style>
