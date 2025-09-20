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
      <div class="text-center mb-16">
        <h1 class="text-4xl md:text-6xl font-bold mb-6 gradient-text">Narxlar</h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          O'zingizga mos rejimni tanlang va AI maslahatlardan foydalaning
        </p>
      </div>

      <div class="grid md:grid-cols-3 gap-8 max-w-6xl mx-auto">
        <div v-for="plan in plans" :key="plan.name" 
             :class="plan.popular ? 'ring-2 ring-primary transform scale-105' : ''"
             class="glass rounded-2xl p-8 hover:scale-105 transition-all duration-300 relative">
          
          <div v-if="plan.popular" class="absolute -top-4 left-1/2 transform -translate-x-1/2">
            <span class="bg-primary px-4 py-1 rounded-full text-sm font-semibold">MASHHUR</span>
          </div>

          <div class="text-center mb-8">
            <h3 :class="'text-' + plan.color + '-400'" class="text-2xl font-bold mb-4">{{ plan.name }}</h3>
            <div class="mb-2">
              <span class="text-4xl font-bold">{{ plan.price }}</span>
              <span class="text-gray-400 ml-1">so'm</span>
            </div>
            <p class="text-gray-400">{{ plan.period }}</p>
          </div>

          <ul class="space-y-3 mb-8">
            <li v-for="feature in plan.features" :key="feature" class="flex items-center">
              <i :class="'text-' + plan.color + '-400'" class="fas fa-check mr-3"></i>
              <span class="text-gray-300">{{ feature }}</span>
            </li>
          </ul>

          <button @click="buyPlan(plan)" 
                  :class="plan.popular ? 'bg-gradient-to-r from-primary to-secondary' : 'bg-gray-700 hover:bg-gray-600'"
                  class="w-full py-4 rounded-lg font-semibold transition-all hover:scale-105">
            {{ plan.name === 'BEPUL' ? 'Boshlash' : 'Sotib Olish' }}
          </button>
        </div>
      </div>

      <!-- FAQ Section -->
      <div class="mt-20">
        <h2 class="text-3xl font-bold text-center mb-12">Tez-tez So'raladigan Savollar</h2>
        <div class="max-w-4xl mx-auto space-y-6">
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2">Token kodi qanday olinadi?</h3>
            <p class="text-gray-300">Pro va Advanced rejimlarni sotib olish uchun @Dier_Ai telegram kanaliga murojaat qiling va to'lov qilgandan so'ng token kodni oling.</p>
          </div>
          
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2">To'lov qanday amalga oshiriladi?</h3>
            <p class="text-gray-300">To'lov Click, Payme, bank o'tkazmalari orqali amalga oshiriladi. Batafsil ma'lumot uchun @Dier_Ai ga murojaat qiling.</p>
          </div>
          
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2">Bepul rejimda qanday cheklovlar bor?</h3>
            <p class="text-gray-300">Bepul rejimda kuniga 10 ta savolga javob olishingiz mumkin va faqat asosiy maslahatlardan foydalanasiz.</p>
          </div>
          
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2">Obunani bekor qilish mumkinmi?</h3>
            <p class="text-gray-300">Ha, istalgan vaqtda obunangizni bekor qilishingiz mumkin. Batafsil ma'lumot uchun yordam xizmatiga murojaat qiling.</p>
          </div>
          
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2">Qaysi toifalardagi maslahatlar mavjud?</h3>
            <p class="text-gray-300">Biz barcha sohalarda maslahat beramiz: biznes, ta'lim, texnologiya, salomatlik, shaxsiy rivojlanish va boshqalar.</p>
          </div>
          
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2">Javoblar qanchalik tez keladi?</h3>
            <p class="text-gray-300">Bepul rejimda javoblar bir necha soniyada, Pro rejimda tezroq, Advanced rejimda esa eng tez va batafsil javoblar beriladi.</p>
          </div>
        </div>
      </div>

      <!-- Contact Section -->
      <div class="mt-20 text-center">
        <div class="glass rounded-2xl p-8 max-w-2xl mx-auto">
          <h2 class="text-2xl font-bold mb-4">Qo'shimcha Savollar Bormi?</h2>
          <p class="text-gray-300 mb-6">
            Agar sizda qo'shimcha savollar bo'lsa, bizning yordam xizmatimizga murojaat qiling.
          </p>
          <a href="https://t.me/Dier_Ai" target="_blank" 
             class="inline-flex items-center bg-blue-600 hover:bg-blue-700 px-6 py-3 rounded-lg font-semibold transition-colors">
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
          price: '50,000',
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
          price: '120,000',
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
