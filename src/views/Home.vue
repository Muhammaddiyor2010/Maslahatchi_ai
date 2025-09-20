<template>
  <div>
    <!-- Token Modal -->
    <TokenModal 
      :show="showTokenModal" 
      :plan="selectedPlan" 
      @close="showTokenModal = false" 
      @success="handleTokenSuccess" 
    />
    <!-- Hero Section -->
    <section class="pt-20 pb-16 px-4">
      <div class="max-w-7xl mx-auto">
        <div class="text-center mb-16">
          <h1 class="text-5xl md:text-7xl font-bold mb-6 gradient-text animate-fade-in">
            Maslahatchi AI
          </h1>
          <p class="text-xl md:text-2xl text-gray-300 mb-8 max-w-3xl mx-auto">
            Professional AI maslahatchi - sizning shaxsiy yordamchingiz barcha masalalarda
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center mb-12">
            <button @click="startChat" class="bg-gradient-to-r from-primary to-secondary px-8 py-4 rounded-full text-lg font-semibold hover:scale-105 transition-transform animate-glow">
              <i class="fas fa-play mr-2"></i>Bepul Boshlash
            </button>
            <router-link to="/pricing" class="border-2 border-primary px-8 py-4 rounded-full text-lg font-semibold hover:bg-primary/10 transition-colors">
              Narxlarni Ko'rish
            </router-link>
          </div>
        </div>

        <!-- Stats -->
        <div class="grid md:grid-cols-4 gap-8 mb-16">
          <div v-for="stat in stats" :key="stat.label" class="text-center glass rounded-2xl p-6 hover:scale-105 transition-transform">
            <i :class="stat.icon + ' text-4xl text-primary mb-4'"></i>
            <h3 class="text-3xl font-bold mb-2">{{ stat.value }}</h3>
            <p class="text-gray-300">{{ stat.label }}</p>
          </div>
        </div>

        <!-- FAQ Section -->
        <div class="grid md:grid-cols-3 gap-8 mb-16">
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
        </div>

        <!-- Plan Selection -->
        <div class="max-w-4xl mx-auto mb-16">
          <h2 class="text-3xl font-bold text-center mb-8">Rejimni Tanlang</h2>
          <div class="grid md:grid-cols-3 gap-6">
            <div @click="selectPlan('free')" :class="{'ring-2 ring-primary': currentPlan === 'free'}" 
                 class="glass rounded-2xl p-6 cursor-pointer hover:scale-105 transition-all">
              <h3 class="text-xl font-bold mb-4 text-green-400">BEPUL</h3>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Kuniga 2 ta savol</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Asosiy maslahatlar</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>24/7 yordam</li>
              </ul>
              <div class="mt-4">
                <span class="text-xs text-green-400">Hozir ishlaydi</span>
              </div>
            </div>
            
            <div @click="selectPlan('pro')" :class="{'ring-2 ring-primary': currentPlan === 'pro' && isAuthenticated}" 
                 class="glass rounded-2xl p-6 cursor-pointer hover:scale-105 transition-all">
              <h3 class="text-xl font-bold mb-4 text-yellow-400">PRO</h3>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-yellow-400 mr-2"></i>Kuniga 50 ta savol</li>
                <li><i class="fas fa-check text-yellow-400 mr-2"></i>Professional maslahatlar</li>
                <li><i class="fas fa-check text-yellow-400 mr-2"></i>Tezkor javoblar</li>
              </ul>
              <div v-if="currentPlan !== 'pro' || !isAuthenticated" class="mt-4">
                <span class="text-xs text-gray-400">Token kiritish kerak</span>
              </div>
            </div>
            
            <div @click="selectPlan('advanced')" :class="{'ring-2 ring-primary': currentPlan === 'advanced' && isAuthenticated}" 
                 class="glass rounded-2xl p-6 cursor-pointer hover:scale-105 transition-all">
              <h3 class="text-xl font-bold mb-4 text-purple-400">ADVANCED</h3>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-purple-400 mr-2"></i>Cheksiz savollar</li>
                <li><i class="fas fa-check text-purple-400 mr-2"></i>Gemini AI texnologiyasi</li>
                <li><i class="fas fa-check text-purple-400 mr-2"></i>Expert darajasida maslahat</li>
              </ul>
              <div v-if="currentPlan !== 'advanced' || !isAuthenticated" class="mt-4">
                <span class="text-xs text-gray-400">Token kiritish kerak</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Chat Interface -->
        <div class="max-w-4xl mx-auto">
          <div class="glass rounded-2xl overflow-hidden">
            <div class="bg-gradient-to-r from-primary to-secondary p-4">
              <div class="flex justify-between items-center">
                <h3 class="text-lg font-semibold">AI Maslahatchi Chat</h3>
                <div class="text-sm">
                  <span v-if="currentPlan !== 'advanced'">
                    {{ dailyUsage }}/{{ usageLimit === Infinity ? '∞' : usageLimit }}
                  </span>
                  <span v-else class="text-green-300">
                    <i class="fas fa-infinity"></i> Cheksiz
                  </span>
                </div>
              </div>
            </div>
            <div class="h-96 overflow-y-auto p-4 space-y-4">
              <div v-if="messages.length === 0" class="text-center text-gray-400 mt-20">
                Salomlashing uchun "Bepul Boshlash" tugmasini bosing
              </div>
              <div v-for="message in messages" :key="message.timestamp" 
                   :class="message.sender === 'user' ? 'text-right' : 'text-left'">
                <div :class="message.sender === 'user' ? 'bg-primary text-white ml-12' : 'bg-gray-700 text-white mr-12'" 
                     class="inline-block p-3 rounded-lg max-w-xs">
                  {{ message.text }}
                </div>
              </div>
              <div v-if="isTyping" class="text-left">
                <div class="bg-gray-700 text-white mr-12 inline-block p-3 rounded-lg">
                  <i class="fas fa-ellipsis-h animate-pulse"></i> Yozmoqda...
                </div>
              </div>
            </div>
            <div class="p-4 border-t border-white/10">
              <div class="flex gap-2">
                <input v-model="currentMessage" @keyup.enter="sendMessage(currentMessage)" 
                       placeholder="Savolingizni yozing..." 
                       :disabled="!canSendMessage"
                       class="flex-1 bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-4 py-2 text-white dark:text-white light:text-gray-900 disabled:opacity-50 disabled:cursor-not-allowed">
                <button @click="sendMessage(currentMessage)" 
                        :disabled="!currentMessage.trim() || !canSendMessage"
                        class="bg-primary px-6 py-2 rounded-lg hover:bg-primary/80 transition-colors disabled:opacity-50 disabled:cursor-not-allowed">
                  <i class="fas fa-paper-plane"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>

<script>
import TokenModal from '../components/TokenModal.vue'

export default {
  name: 'Home',
  components: {
    TokenModal
  },
  data() {
    return {
      currentPlan: 'free',
      selectedPlan: 'pro', // Token modal uchun tanlangan plan
      showTokenModal: false,
      messages: [],
      currentMessage: '',
      isTyping: false,
      dailyUsage: 0,
      lastUsageDate: null,
      isAuthenticated: false,
      geminiApiKey: 'AIzaSyDPT4MGKHz1JOkLd5_3rlXdKeMXSLIxd8E',
      stats: [
        { icon: 'fas fa-users', value: '10,000+', label: 'Foydalanuvchilar' },
        { icon: 'fas fa-comments', value: '50,000+', label: 'Maslahatlar' },
        { icon: 'fas fa-star', value: '4.9/5', label: 'Reyting' },
        { icon: 'fas fa-clock', value: '24/7', label: 'Yordam' }
      ]
    }
  },
  computed: {
    usageLimit() {
      switch(this.currentPlan) {
        case 'free': return 2;
        case 'pro': return 50;
        case 'advanced': return Infinity;
        default: return 2;
      }
    },
    remainingUsage() {
      return Math.max(0, this.usageLimit - this.dailyUsage);
    },
    canSendMessage() {
      if (this.currentPlan === 'advanced') return true;
      return this.dailyUsage < this.usageLimit;
    }
  },
  mounted() {
    this.loadUsageData();
  },
  methods: {
    loadUsageData() {
      const today = new Date().toDateString();
      const savedData = localStorage.getItem('usageData');
      
      if (savedData) {
        const data = JSON.parse(savedData);
        if (data.date === today) {
          this.dailyUsage = data.usage;
          this.lastUsageDate = data.date;
        } else {
          this.dailyUsage = 0;
          this.lastUsageDate = today;
        }
      } else {
        this.lastUsageDate = today;
      }
    },
    saveUsageData() {
      const data = {
        date: new Date().toDateString(),
        usage: this.dailyUsage
      };
      localStorage.setItem('usageData', JSON.stringify(data));
    },
    startChat() {
      if (this.currentPlan === 'free') {
        // Bot xabarini to'g'ridan-to'g'ri qo'shamiz, recursive chaqiruv emas
        this.messages.push({ 
          text: "Salom! Maslahatchi AI ga xush kelibsiz. Sizga qanday yordam bera olaman?", 
          sender: 'bot', 
          timestamp: new Date() 
        });
      } else if (this.currentPlan === 'pro' || this.currentPlan === 'advanced') {
        if (this.isAuthenticated) {
          // Agar allaqachon authenticated bo'lsa, to'g'ridan-to'g'ri chat boshlash
          this.messages.push({ 
            text: "Salom! Maslahatchi AI ga xush kelibsiz. Sizga qanday yordam bera olaman?", 
            sender: 'bot', 
            timestamp: new Date() 
          });
        } else {
          // Agar authenticated bo'lmasa, token modal ochish
          this.showTokenModal = true;
        }
      }
    },
    async sendMessage(text, sender = 'user') {
      if (sender === 'user') {
        if (!this.canSendMessage) {
          alert(`Sizning kunlik limit (${
            this.currentPlan === 'free' ? '2 ta' : 
            this.currentPlan === 'pro' ? '50 ta' : 'Cheksiz'
          }) tugadi. Keyingi kunda qayta urinib ko'ring yoki rejimni yangilang.`);
          return;
        }
        
        this.dailyUsage++;
        this.saveUsageData();
      }
      
      this.messages.push({ text, sender, timestamp: new Date() });
      
      if (sender === 'user') {
        this.currentMessage = '';
        this.isTyping = true;
        
        try {
          let response;
          // Barcha rejimlarda haqiqiy Gemini AI ishlatamiz
          console.log('Using Gemini API for response...');
          response = await this.getGeminiResponse(text);
          
          setTimeout(() => {
            this.isTyping = false;
            // Bot javobini to'g'ridan-to'g'ri qo'shamiz, recursive chaqiruv emas
            this.messages.push({ text: response, sender: 'bot', timestamp: new Date() });
          }, 1500);
        } catch (error) {
          console.error('Error in sendMessage:', error);
          this.isTyping = false;
          // Xatolik javobini ham to'g'ridan-to'g'ri qo'shamiz
          this.messages.push({ text: "Uzr, xatolik yuz berdi. Iltimos, qayta urinib ko'ring.", sender: 'bot', timestamp: new Date() });
        }
      }
    },
    async getGeminiResponse(message) {
      try {
        console.log('Sending request to Gemini API...');
        console.log('API Key:', this.geminiApiKey.substring(0, 10) + '...');
        console.log('Message:', message);
        
        const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${this.geminiApiKey}`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            contents: [{
              parts: [{
                text: `Siz professional AI maslahatchisiz. Foydalanuvchi savoliga o'zbek tilida batafsil va foydali javob bering: ${message}`
              }]
            }]
          })
        });
        
        console.log('Gemini API response status:', response.status);
        
        if (!response.ok) {
          const errorText = await response.text();
          console.error('HTTP Error Response:', errorText);
          throw new Error(`HTTP error! status: ${response.status}, message: ${errorText}`);
        }
        
        const data = await response.json();
        console.log('Gemini API response data:', data);
        
        if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts) {
          const geminiText = data.candidates[0].content.parts[0].text;
          console.log('Gemini response text:', geminiText);
          return geminiText;
        } else if (data.error) {
          console.error('Gemini API Error:', data.error);
          throw new Error(`Gemini API Error: ${data.error.message || 'Unknown error'}`);
        } else {
          console.error('Invalid Gemini response structure:', data);
          throw new Error('Invalid response structure from Gemini API');
        }
      } catch (error) {
        console.error('Gemini API error:', error);
        console.log('Falling back to basic response...');
        return `Uzr, AI xizmati vaqtincha ishlamayapti. Xatolik: ${error.message}. Iltimos, birozdan so'ng qayta urinib ko'ring.`;
      }
    },
    handleTokenSuccess(plan) {
      this.isAuthenticated = true;
      this.currentPlan = plan; // Update currentPlan based on successful token
      
      // PRO rejimga o'tganda limit o'zgarsin
      if (plan === 'pro') {
        this.dailyUsage = 0; // PRO rejimda yangi limit bilan boshlash
      } else if (plan === 'advanced') {
        this.dailyUsage = 0; // ADVANCED rejimda cheksiz
      }
      
      // Success xabarini to'g'ridan-to'g'ri qo'shamiz
      this.messages.push({ 
        text: `${plan.toUpperCase()} rejim faollashtirildi! Endi ${plan === 'pro' ? 'kuniga 50 ta' : 'cheksiz'} savol berishingiz mumkin.`, 
        sender: 'bot', 
        timestamp: new Date() 
      });
      this.saveUsageData();
    },
    selectPlan(plan) {
      if (plan === 'free') {
        // FREE rejimni to'g'ridan-to'g'ri tanlash mumkin
        this.currentPlan = 'free';
        this.isAuthenticated = false;
        console.log('FREE rejim tanlandi');
      } else if (plan === 'pro' || plan === 'advanced') {
        if (this.isAuthenticated && this.currentPlan === plan) {
          // Agar allaqachon authenticated bo'lsa, hech narsa qilmaymiz
          console.log(`${plan.toUpperCase()} rejim allaqachon faol`);
        } else {
          // Tanlangan planni saqlash va token modal ochish
          this.selectedPlan = plan;
          this.showTokenModal = true;
          console.log(`${plan.toUpperCase()} rejim uchun token modal ochildi`);
        }
      }
    },
    contactTelegram() {
      window.open('https://t.me/Dier_Ai', '_blank');
    }
  }
}
</script>

<style scoped>
.text-primary {
  color: #6366f1;
}
</style>