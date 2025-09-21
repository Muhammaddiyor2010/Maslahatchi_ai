<template>
  <div>
    <!-- Hero Section -->
    <section class="pt-20 pb-16 px-4">
      <div class="max-w-7xl mx-auto">
        <div class="text-center mb-16 px-4">
          <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl xl:text-7xl font-bold mb-4 sm:mb-6 gradient-text animate-fade-in-down">
            Maslahatchi AI
          </h1>
          <p class="text-base sm:text-lg md:text-xl lg:text-2xl text-gray-300 mb-6 sm:mb-8 max-w-3xl mx-auto leading-relaxed animate-fade-in-up animate-delay-200">
            Professional AI maslahatchi - sizning shaxsiy yordamchingiz barcha masalalarda
          </p>
          <div class="flex flex-col sm:flex-row gap-3 sm:gap-4 justify-center mb-8 sm:mb-12 px-4 animate-fade-in-up animate-delay-400">
            <router-link to="/chat" class="bg-gradient-to-r from-primary to-secondary px-6 sm:px-8 py-3 sm:py-4 rounded-full text-base sm:text-lg font-semibold hover:scale-105 transition-transform animate-glow text-center">
              <i class="fas fa-comments mr-2"></i>Chat Boshlash
            </router-link>
            <router-link to="/pricing" class="border-2 border-primary px-6 sm:px-8 py-3 sm:py-4 rounded-full text-base sm:text-lg font-semibold hover:bg-primary/10 transition-colors text-center">
              Narxlarni Ko'rish
            </router-link>
          </div>
        </div>

        <!-- Stats -->
        <div class="grid grid-cols-2 sm:grid-cols-2 md:grid-cols-4 gap-4 sm:gap-6 md:gap-8 mb-12 sm:mb-16 px-4">
          <div v-for="(stat, index) in stats" :key="stat.label" 
               :class="'text-center glass rounded-xl sm:rounded-2xl p-4 sm:p-6 hover:scale-105 transition-transform animate-slide-in-up animate-delay-' + ((index + 1) * 100)">
            <i :class="stat.icon + ' text-2xl sm:text-3xl md:text-4xl text-primary mb-2 sm:mb-4'"></i>
            <h3 class="text-xl sm:text-2xl md:text-3xl font-bold mb-1 sm:mb-2">{{ stat.value }}</h3>
            <p class="text-gray-300 text-sm sm:text-base">{{ stat.label }}</p>
          </div>
        </div>

        <!-- FAQ Section -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6 md:gap-8 mb-12 sm:mb-16 px-4">
          <div class="glass rounded-lg p-4 sm:p-6 animate-slide-in-left animate-delay-600">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">To'lov qanday amalga oshiriladi?</h3>
            <p class="text-gray-300 text-sm sm:text-base">To'lov Click, Payme, bank o'tkazmalari orqali amalga oshiriladi. Batafsil ma'lumot uchun @Dier_Ai ga murojaat qiling.</p>
          </div>
          <div class="glass rounded-lg p-4 sm:p-6 animate-fade-in-up animate-delay-700">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Bepul rejimda qanday cheklovlar bor?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Bepul rejimda kuniga 10 ta savolga javob olishingiz mumkin va faqat asosiy maslahatlardan foydalanasiz.</p>
          </div>
          <div class="glass rounded-lg p-4 sm:p-6 sm:col-span-2 lg:col-span-1 animate-slide-in-right animate-delay-800">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Obunani bekor qilish mumkinmi?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Ha, istalgan vaqtda obunangizni bekor qilishingiz mumkin. Batafsil ma'lumot uchun yordam xizmatiga murojaat qiling.</p>
          </div>
        </div>

        <!-- Help Section -->
        <div class="text-center mb-12 sm:mb-16 px-4">
          <div class="glass rounded-xl sm:rounded-2xl p-6 sm:p-8 max-w-2xl mx-auto animate-slide-in-left animate-delay-900">
            <i class="fas fa-question-circle text-3xl sm:text-4xl md:text-5xl text-primary mb-3 sm:mb-4"></i>
            <h2 class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4">Savollaringiz bormi?</h2>
            <p class="text-gray-300 mb-4 sm:mb-6 text-sm sm:text-base">
              Batafsil qo'llanma, FAQ va qo'llab-quvvatlash xizmatimizdan foydalaning
            </p>
            <router-link to="/help" 
                         class="inline-flex items-center bg-primary hover:bg-primary/80 px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-semibold transition-colors text-sm sm:text-base">
              <i class="fas fa-life-ring mr-2"></i>
              Yordam Markaziga O'tish
            </router-link>
          </div>
        </div>

        <!-- Chat CTA Section -->
        <div class="max-w-4xl mx-auto mb-12 sm:mb-16 px-4">
          <div class="glass rounded-xl sm:rounded-2xl p-6 sm:p-8 md:p-12 text-center animate-slide-in-right animate-delay-1000">
            <i class="fas fa-robot text-4xl sm:text-5xl md:text-6xl text-primary mb-4 sm:mb-6"></i>
            <h2 class="text-2xl sm:text-3xl font-bold mb-3 sm:mb-4">AI Maslahatchi Chat</h2>
            <p class="text-base sm:text-lg md:text-xl text-gray-300 mb-6 sm:mb-8 max-w-2xl mx-auto">
              Professional AI maslahatchi bilan suhbatlashib, barcha savollaringizga javob oling
            </p>
            <router-link to="/chat" 
                         class="inline-flex items-center bg-gradient-to-r from-primary to-secondary px-6 sm:px-8 py-3 sm:py-4 rounded-lg text-base sm:text-lg font-semibold hover:scale-105 transition-transform">
              <i class="fas fa-comments mr-2"></i>
              Chat Boshlash
            </router-link>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      stats: [
        { icon: 'fas fa-users', value: '10,000+', label: 'Foydalanuvchilar' },
        { icon: 'fas fa-comments', value: '50,000+', label: 'Maslahatlar' },
        { icon: 'fas fa-star', value: '4.9/5', label: 'Reyting' },
        { icon: 'fas fa-clock', value: '24/7', label: 'Yordam' }
      ]
    }
  }
}
</script>

<style scoped>
.text-primary {
  color: #6366f1;
}

.text-secondary {
  color: #8b5cf6;
}

.gradient-text {
  background: linear-gradient(135deg, #6366f1, #8b5cf6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.glass {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.animate-fade-in {
  animation: fadeIn 1s ease-in-out;
}

.animate-glow {
  animation: glow 2s ease-in-out infinite alternate;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes glow {
  from {
    box-shadow: 0 0 20px rgba(99, 102, 241, 0.5);
  }
  to {
    box-shadow: 0 0 30px rgba(99, 102, 241, 0.8);
  }
}
</style>