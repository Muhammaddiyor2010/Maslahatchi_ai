<template>
  <div class="pt-24 pb-16 px-4">
    <!-- Token Modal -->
    <TokenModal 
      :show="showTokenModal" 
      :plan="selectedPlan" 
      @close="showTokenModal = false" 
      @success="handleTokenSuccess" 
    />
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-12 sm:mb-16 px-4">
        <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold mb-4 sm:mb-6 gradient-text animate-fade-in-down">Narxlar</h1>
        <p class="text-base sm:text-lg md:text-xl text-gray-300 max-w-3xl mx-auto leading-relaxed animate-fade-in-up animate-delay-200">
          O'zingizga mos rejimni tanlang va AI maslahatlardan foydalaning
        </p>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6 md:gap-8 max-w-6xl mx-auto px-4">
        <div v-for="(plan, index) in plans" :key="plan.name" 
             :class="plan.popular ? 'ring-2 ring-primary transform scale-105' : ''"
             :class="'glass rounded-xl sm:rounded-2xl p-4 sm:p-6 md:p-8 hover:scale-105 transition-all duration-300 relative animate-slide-in-up animate-delay-' + ((index + 1) * 200)">
          
          <div v-if="plan.popular" class="absolute -top-3 sm:-top-4 left-1/2 transform -translate-x-1/2">
            <span class="bg-primary px-3 sm:px-4 py-1 rounded-full text-xs sm:text-sm font-semibold">MASHHUR</span>
          </div>

          <div class="text-center mb-6 sm:mb-8">
            <h3 :class="'text-' + plan.color + '-400'" class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4">{{ plan.name }}</h3>
            <div class="mb-2">
              <span class="text-2xl sm:text-3xl md:text-4xl font-bold">{{ plan.price }}</span>
              <span class="text-gray-400 ml-1 text-sm sm:text-base">so'm</span>
            </div>
            <p class="text-gray-400 text-sm sm:text-base">{{ plan.period }}</p>
          </div>

          <ul class="space-y-2 sm:space-y-3 mb-6 sm:mb-8">
            <li v-for="feature in plan.features" :key="feature" class="flex items-center">
              <i :class="'text-' + plan.color + '-400'" class="fas fa-check mr-2 sm:mr-3 text-sm sm:text-base"></i>
              <span class="text-gray-300 text-sm sm:text-base">{{ feature }}</span>
            </li>
          </ul>

          <button @click="buyPlan(plan)" 
                  :class="plan.popular ? 'bg-gradient-to-r from-primary to-secondary' : 'bg-gray-700 hover:bg-gray-600'"
                  class="w-full py-3 sm:py-4 rounded-lg font-semibold transition-all hover:scale-105 text-sm sm:text-base">
            {{ plan.name === 'BEPUL' ? 'Boshlash' : 'Sotib Olish' }}
          </button>
        </div>
      </div>

      <!-- FAQ Section -->
      <div class="mt-16 sm:mt-20 px-4">
        <h2 class="text-2xl sm:text-3xl font-bold text-center mb-8 sm:mb-12 animate-fade-in-up animate-delay-800">Tez-tez So'raladigan Savollar</h2>
        <div class="max-w-4xl mx-auto space-y-4 sm:space-y-6">
          <div class="glass rounded-lg p-4 sm:p-6 animate-slide-in-left animate-delay-900">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Token kodi qanday olinadi?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Pro va Advanced rejimlarni sotib olish uchun @Dier_Ai telegram kanaliga murojaat qiling va to'lov qilgandan so'ng token kodni oling.</p>
          </div>
          
          <div class="glass rounded-lg p-4 sm:p-6 animate-fade-in-up animate-delay-1000">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">To'lov qanday amalga oshiriladi?</h3>
            <p class="text-gray-300 text-sm sm:text-base">To'lov Click, Payme, bank o'tkazmalari orqali amalga oshiriladi. Batafsil ma'lumot uchun @Dier_Ai ga murojaat qiling.</p>
          </div>
          
          <div class="glass rounded-lg p-4 sm:p-6 animate-slide-in-right animate-delay-1100">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Bepul rejimda qanday cheklovlar bor?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Bepul rejimda kuniga 10 ta savolga javob olishingiz mumkin va faqat asosiy maslahatlardan foydalanasiz.</p>
          </div>
          
          <div class="glass rounded-lg p-4 sm:p-6 animate-slide-in-left animate-delay-1200">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Obunani bekor qilish mumkinmi?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Ha, istalgan vaqtda obunangizni bekor qilishingiz mumkin. Batafsil ma'lumot uchun yordam xizmatiga murojaat qiling.</p>
          </div>
          
          <div class="glass rounded-lg p-4 sm:p-6 animate-fade-in-up animate-delay-1300">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Qaysi toifalardagi maslahatlar mavjud?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Biz barcha sohalarda maslahat beramiz: biznes, ta'lim, texnologiya, salomatlik, shaxsiy rivojlanish va boshqalar.</p>
          </div>
          
          <div class="glass rounded-lg p-4 sm:p-6 animate-slide-in-right animate-delay-1400">
            <h3 class="font-semibold mb-2 text-sm sm:text-base">Javoblar qanchalik tez keladi?</h3>
            <p class="text-gray-300 text-sm sm:text-base">Bepul rejimda javoblar bir necha soniyada, Pro rejimda tezroq, Advanced rejimda esa eng tez va batafsil javoblar beriladi.</p>
          </div>
        </div>
      </div>

      <!-- Contact Section -->
      <div class="mt-16 sm:mt-20 text-center px-4">
        <div class="glass rounded-xl sm:rounded-2xl p-6 sm:p-8 max-w-2xl mx-auto animate-fade-in-up animate-delay-1500">
          <h2 class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4">Qo'shimcha Savollar Bormi?</h2>
          <p class="text-gray-300 mb-4 sm:mb-6 text-sm sm:text-base">
            Agar sizda qo'shimcha savollar bo'lsa, bizning yordam xizmatimizga murojaat qiling.
          </p>
          <a href="https://t.me/Dier_Ai" target="_blank" 
             class="inline-flex items-center bg-blue-600 hover:bg-blue-700 px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-semibold transition-colors text-sm sm:text-base">
            <i class="fab fa-telegram mr-2"></i>Telegram orqali yozing
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TokenModal from '../components/TokenModal.vue'

export default {
  name: 'Pricing',
  components: {
    TokenModal
  },
  data() {
    return {
      showTokenModal: false,
      selectedPlan: 'pro',
      plans: [
        {
          name: 'BEPUL',
          price: '0',
          period: 'Abadiy',
          color: 'green',
          features: [
            'Kuniga 10 ta savol',
            'Asosiy maslahatlar',
            'Email yordam',
            'Mobil ilova'
          ],
          popular: false
        },
        {
          name: 'PRO',
          price: '2,000',
          period: 'Oyiga',
          color: 'blue',
          features: [
            'Cheksiz savollar',
            'Professional maslahatlar',
            'Prioritet yordam',
            'Ilg\'or tahlil',
            'API kirish'
          ],
          popular: true
        },
        {
          name: 'ADVANCED',
          price: '20,000',
          period: 'Oyiga',
          color: 'purple',
          features: [
            'Barcha PRO funksiyalar',
            'Shaxsiy maslahatchi',
            'Maxsus yechimlar',
            'White-label',
            'Onboarding yordam'
          ],
          popular: false
        }
      ]
    }
  },
  methods: {
    buyPlan(plan) {
      if (plan.name === 'BEPUL') {
        alert('Bepul rejim allaqachon faol!');
      } else if (plan.name === 'PRO') {
        this.selectedPlan = 'pro';
        this.showTokenModal = true;
      } else if (plan.name === 'ADVANCED') {
        this.selectedPlan = 'advanced';
        this.showTokenModal = true;
      }
    },
    handleTokenSuccess(plan) {
      // Show success message and redirect to home
      alert(`${plan.toUpperCase()} rejim muvaffaqiyatli faollashtirildi! Endi barcha premium xususiyatlardan foydalanishingiz mumkin.`);
      this.$router.push('/');
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
</style>
