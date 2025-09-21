<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <!-- Hero Section -->
      <div class="text-center mb-6 sm:mb-8 px-4">
        <h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold mb-4 sm:mb-6 gradient-text animate-fade-in-down">AI Maslahatchi Chat</h1>
        <p class="text-base sm:text-lg md:text-xl text-gray-300 max-w-3xl mx-auto leading-relaxed animate-fade-in-up animate-delay-200">
          Professional AI maslahatchi bilan suhbatlashib, barcha savollaringizga javob oling
        </p>
      </div>

      <!-- Plan Selection -->
      <div class="max-w-4xl mx-auto mb-6 sm:mb-8 px-4">
        <h2 class="text-xl sm:text-2xl font-bold text-center mb-4 sm:mb-6 animate-fade-in-up animate-delay-300">Rejimni Tanlang</h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6">
          <div @click="selectPlan('free')" :class="{'ring-2 ring-primary': currentPlan === 'free'}" 
               class="glass rounded-xl sm:rounded-2xl p-4 sm:p-6 cursor-pointer hover:scale-105 transition-all animate-slide-in-left animate-delay-400">
            <h3 class="text-lg sm:text-xl font-bold mb-3 sm:mb-4 text-green-400">BEPUL</h3>
            <ul class="space-y-1 sm:space-y-2 text-xs sm:text-sm text-gray-300">
              <li><i class="fas fa-times text-red-400 mr-2"></i>AI maslahatchi yo'q</li>
              <li><i class="fas fa-check text-green-400 mr-2"></i>Sayt ko'rish</li>
              <li><i class="fas fa-check text-green-400 mr-2"></i>Rejimlar haqida ma'lumot</li>
            </ul>
            <div class="mt-3 sm:mt-4">
              <span class="text-xs text-red-400">AI ishlamaydi</span>
            </div>
          </div>
          
          <div @click="selectPlan('pro')" :class="{'ring-2 ring-primary': currentPlan === 'pro' && isAuthenticated}" 
               class="glass rounded-xl sm:rounded-2xl p-4 sm:p-6 cursor-pointer hover:scale-105 transition-all animate-fade-in-up animate-delay-500">
            <h3 class="text-lg sm:text-xl font-bold mb-3 sm:mb-4 text-yellow-400">PRO</h3>
            <ul class="space-y-1 sm:space-y-2 text-xs sm:text-sm text-gray-300">
              <li><i class="fas fa-check text-yellow-400 mr-2"></i>Kuniga 50 ta savol</li>
              <li><i class="fas fa-check text-yellow-400 mr-2"></i>Professional maslahatlar</li>
              <li><i class="fas fa-check text-yellow-400 mr-2"></i>Tezkor javoblar</li>
            </ul>
            <div v-if="currentPlan !== 'pro' || !isAuthenticated" class="mt-3 sm:mt-4">
              <span class="text-xs text-gray-400">Token kiritish kerak</span>
            </div>
          </div>
          
          <div @click="selectPlan('advanced')" :class="{'ring-2 ring-primary': currentPlan === 'advanced' && isAuthenticated}" 
               class="glass rounded-xl sm:rounded-2xl p-4 sm:p-6 cursor-pointer hover:scale-105 transition-all sm:col-span-2 lg:col-span-1 animate-slide-in-right animate-delay-600">
            <h3 class="text-lg sm:text-xl font-bold mb-3 sm:mb-4 text-purple-400">ADVANCED</h3>
            <ul class="space-y-1 sm:space-y-2 text-xs sm:text-sm text-gray-300">
              <li><i class="fas fa-check text-purple-400 mr-2"></i>Cheksiz savollar</li>
              <li><i class="fas fa-check text-purple-400 mr-2"></i>Gemini AI texnologiyasi</li>
              <li><i class="fas fa-check text-purple-400 mr-2"></i>Expert darajasida maslahat</li>
            </ul>
            <div v-if="currentPlan !== 'advanced' || !isAuthenticated" class="mt-3 sm:mt-4">
              <span class="text-xs text-gray-400">Token kiritish kerak</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Chat Interface -->
      <div class="max-w-4xl mx-auto px-4">
        <div ref="chatContainer" class="glass rounded-xl sm:rounded-2xl overflow-hidden animate-fade-in-up animate-delay-700">
          <div class="bg-gradient-to-r from-primary to-secondary p-3 sm:p-4">
            <div class="flex justify-between items-center">
              <h3 class="text-base sm:text-lg font-semibold">AI Maslahatchi Chat</h3>
              <div class="text-xs sm:text-sm">
                <span v-if="currentPlan !== 'advanced'">
                  {{ dailyUsage }}/{{ usageLimit === Infinity ? '∞' : usageLimit }}
                </span>
                <span v-else class="text-green-300">
                  <i class="fas fa-infinity"></i> Cheksiz
                </span>
              </div>
            </div>
          </div>
          <div class="h-64 sm:h-80 md:h-96 overflow-y-auto p-3 sm:p-4 space-y-3 sm:space-y-4">
            <div v-if="messages.length === 0" class="text-center text-gray-400 mt-12 sm:mt-16 md:mt-20">
              <i class="fas fa-robot text-2xl sm:text-3xl md:text-4xl mb-3 sm:mb-4"></i>
              <p class="text-sm sm:text-base">Salom! Men sizning AI maslahatchiingizman.</p>
              <p class="text-xs sm:text-sm mt-1 sm:mt-2">Savolingizni yozing va men sizga yordam beraman.</p>
            </div>
            <div v-for="message in messages" :key="message.timestamp" 
                 :class="message.sender === 'user' ? 'text-right' : 'text-left'">
              <div :class="message.sender === 'user' ? 'bg-primary text-white ml-6 sm:ml-12' : 'bg-gray-700 text-white mr-6 sm:mr-12'" 
                   class="inline-block p-2 sm:p-3 rounded-lg max-w-xs sm:max-w-sm text-sm sm:text-base leading-relaxed">
                <div v-if="message.sender === 'ai'" v-html="formatAIMessage(message.text)"></div>
                <div v-else>{{ message.text }}</div>
              </div>
            </div>
            <div v-if="isTyping" class="text-left">
              <div class="bg-gray-700 text-white mr-6 sm:mr-12 inline-block p-2 sm:p-3 rounded-lg text-sm sm:text-base">
                <i class="fas fa-ellipsis-h animate-pulse"></i> Yozmoqda...
              </div>
            </div>
          </div>
          <div class="p-3 sm:p-4 border-t border-white/10">
            <div class="flex gap-2">
              <input ref="chatInput" v-model="currentMessage" @keyup.enter="sendMessage(currentMessage)" 
                     placeholder="Savolingizni yozing..." 
                     :disabled="!canSendMessage"
                     class="flex-1 bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-3 sm:px-4 py-2 text-white dark:text-white light:text-gray-900 disabled:opacity-50 disabled:cursor-not-allowed text-sm sm:text-base">
              <button @click="sendMessage(currentMessage)" 
                      :disabled="!currentMessage.trim() || !canSendMessage"
                      class="bg-primary px-4 sm:px-6 py-2 rounded-lg hover:bg-primary/80 transition-colors disabled:opacity-50 disabled:cursor-not-allowed">
                <i class="fas fa-paper-plane text-sm sm:text-base"></i>
              </button>
            </div>
            <div v-if="!canSendMessage" class="mt-2 text-center">
              <p class="text-xs sm:text-sm text-gray-400">
                <span v-if="currentPlan === 'free'">AI maslahatchi faqat PRO va ADVANCED rejalarda mavjud</span>
                <span v-else-if="!isAuthenticated">Token kiritish kerak</span>
                <span v-else-if="dailyUsage >= usageLimit">Kunlik limit tugagan</span>
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- Quick Actions -->
      <div class="max-w-4xl mx-auto mt-6 sm:mt-8 px-4">
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6">
          <div class="glass rounded-lg p-4 sm:p-6 text-center animate-slide-in-left animate-delay-800">
            <i class="fas fa-lightbulb text-2xl sm:text-3xl text-yellow-400 mb-3 sm:mb-4"></i>
            <h3 class="font-bold mb-2 text-sm sm:text-base">Maslahat Olish</h3>
            <p class="text-gray-300 text-xs sm:text-sm">Har qanday sohada professional maslahat oling</p>
          </div>
          <div class="glass rounded-lg p-4 sm:p-6 text-center animate-fade-in-up animate-delay-900">
            <i class="fas fa-question-circle text-2xl sm:text-3xl text-blue-400 mb-3 sm:mb-4"></i>
            <h3 class="font-bold mb-2 text-sm sm:text-base">Savol Berish</h3>
            <p class="text-gray-300 text-xs sm:text-sm">Barcha savollaringizga tez va aniq javob oling</p>
          </div>
          <div class="glass rounded-lg p-4 sm:p-6 text-center sm:col-span-2 lg:col-span-1 animate-slide-in-right animate-delay-1000">
            <i class="fas fa-graduation-cap text-2xl sm:text-3xl text-green-400 mb-3 sm:mb-4"></i>
            <h3 class="font-bold mb-2 text-sm sm:text-base">O'rganish</h3>
            <p class="text-gray-300 text-xs sm:text-sm">Yangi bilimlar va ko'nikmalar oling</p>
          </div>
        </div>
      </div>

      <!-- Token Modal -->
      <TokenModal 
        :show="showTokenModal" 
        :plan="selectedPlan" 
        @close="showTokenModal = false" 
        @success="handleTokenSuccess" 
      />
    </div>
  </div>
</template>

<script>
import TokenModal from '../components/TokenModal.vue'

export default {
  name: 'Chat',
  components: {
    TokenModal
  },
  data() {
    return {
      currentPlan: 'free',
      selectedPlan: 'pro',
      showTokenModal: false,
      messages: [],
      currentMessage: '',
      isTyping: false,
      dailyUsage: 0,
      lastUsageDate: null,
      isAuthenticated: false,
      geminiApiKey: 'AIzaSyDPT4MGKHz1JOkLd5_3rlXdKeMXSLIxd8E',
      fallbackApiKey: 'AIzaSyCSq12aGvnUxJHF4ZZKBSU1yrEo8ekurdM'
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
      if (this.currentPlan === 'free') return false;
      if (!this.isAuthenticated) return false;
      return this.dailyUsage < this.usageLimit;
    }
  },
  mounted() {
    this.loadUserData();
    this.checkDailyUsage();
  },
  methods: {
    selectPlan(plan) {
      if (plan === 'free') {
        this.currentPlan = 'free';
        this.isAuthenticated = false;
        return;
      }
      
      this.selectedPlan = plan;
      this.showTokenModal = true;
    },
    handleTokenSuccess(plan) {
      this.currentPlan = plan;
      this.isAuthenticated = true;
      this.showTokenModal = false;
      this.loadUserData();
    },
    loadUserData() {
      const savedPlan = localStorage.getItem('userPlan');
      const savedAuth = localStorage.getItem('isAuthenticated');
      const savedUsage = localStorage.getItem('dailyUsage');
      const savedDate = localStorage.getItem('lastUsageDate');
      
      if (savedPlan && savedAuth === 'true') {
        this.currentPlan = savedPlan;
        this.isAuthenticated = true;
        this.dailyUsage = parseInt(savedUsage) || 0;
        this.lastUsageDate = savedDate;
      }
    },
    checkDailyUsage() {
      const today = new Date().toDateString();
      if (this.lastUsageDate !== today) {
        this.dailyUsage = 0;
        this.lastUsageDate = today;
        this.saveUserData();
      }
    },
    saveUserData() {
      localStorage.setItem('userPlan', this.currentPlan);
      localStorage.setItem('isAuthenticated', this.isAuthenticated.toString());
      localStorage.setItem('dailyUsage', this.dailyUsage.toString());
      localStorage.setItem('lastUsageDate', this.lastUsageDate);
    },
    async sendMessage(message) {
      if (!message.trim() || !this.canSendMessage) return;
      
      const userMessage = {
        text: message,
        sender: 'user',
        timestamp: Date.now()
      };
      
      this.messages.push(userMessage);
      this.currentMessage = '';
      this.isTyping = true;
      
      try {
        const response = await this.getAIResponse(message);
        const aiMessage = {
          text: response,
          sender: 'ai',
          timestamp: Date.now()
        };
        
        this.messages.push(aiMessage);
        this.dailyUsage++;
        this.saveUserData();
      } catch (error) {
        console.error('AI response error:', error);
        let errorText = 'Kechirasiz, xatolik yuz berdi. Qaytadan urinib ko\'ring.';
        
        // Xatolik turiga qarab turli xabarlar
        if (error.message.includes('API request failed')) {
          errorText = 'AI xizmati vaqtincha ishlamayapti. Iltimos, keyinroq urinib ko\'ring.';
        } else if (error.message.includes('Invalid API response')) {
          errorText = 'AI javobida xatolik. Qaytadan urinib ko\'ring.';
        } else if (error.message.includes('AI xizmati hozircha mavjud emas')) {
          errorText = 'AI xizmati hozircha mavjud emas. Iltimos, keyinroq urinib ko\'ring.';
        }
        
        const errorMessage = {
          text: errorText,
          sender: 'ai',
          timestamp: Date.now()
        };
        this.messages.push(errorMessage);
      } finally {
        this.isTyping = false;
        this.scrollToBottom();
      }
    },
    async getAIResponse(message) {
      const prompt = `Siz professional maslahatchi AI siz. Foydalanuvchi sizga savol berdi: "${message}". 

Muhim talablar:
1. O'zbek tilida javob bering
2. Javob o'rtacha uzunlikda bo'lsin (3-5 jumla, 50-100 so'z)
3. ** yoki * belgilarini ishlatmang
4. Oddiy va tushunarli til ishlating
5. Professional va foydali maslahat bering
6. Odamga o'xshab, tabiiy javob bering
7. Javobni to'g'ridan-to'g'ri bering, qo'shimcha formatlashsiz
8. Har bir jumla aniq va tushunarli bo'lsin

Javob bering:`;

      // Birinchi tokendan urinish
      try {
        return await this.tryApiRequest(this.geminiApiKey, prompt);
      } catch (error) {
        console.log('Birinchi token ishlamadi, ikkinchi tokendan urinamiz...', error);
        
        // Ikkinchi tokendan urinish
        try {
          return await this.tryApiRequest(this.fallbackApiKey, prompt);
        } catch (fallbackError) {
          console.error('Ikkala token ham ishlamadi:', fallbackError);
          
          // Mock response berish
          return this.getMockResponse(message);
        }
      }
    },
    
    async tryApiRequest(apiKey, prompt) {
      // Birinchi urinish - gemini-1.5-flash
      let response;
      try {
        response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            contents: [{
              parts: [{
                text: prompt
              }]
            }]
          })
        });
      } catch (error) {
        // Ikkinchi urinish - gemini-pro
        response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${apiKey}`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            contents: [{
              parts: [{
                text: prompt
              }]
            }]
          })
        });
      }
      
      if (!response.ok) {
        const errorText = await response.text();
        console.error('API Error Response:', errorText);
        throw new Error(`API request failed with status: ${response.status} - ${errorText}`);
      }
      
      const data = await response.json();
      console.log('API Response:', data);
      
      if (!data.candidates || !data.candidates[0] || !data.candidates[0].content) {
        console.error('Invalid API response format:', data);
        throw new Error('Invalid API response format');
      }
      
      let aiResponse = data.candidates[0].content.parts[0].text;
      
      // ** belgilarini yo'qotish
      aiResponse = aiResponse.replace(/\*\*/g, '');
      aiResponse = aiResponse.replace(/\*/g, '');
      
      // Boshqa formatlash belgilarini yo'qotish
      aiResponse = aiResponse.replace(/#/g, '');
      aiResponse = aiResponse.replace(/`/g, '');
      aiResponse = aiResponse.replace(/~/g, '');
      
      // Ortiqcha bo'shliqlarni tozalash
      aiResponse = aiResponse.replace(/\s+/g, ' ').trim();
      
      // Javobni qisqartirish (agar juda uzun bo'lsa)
      if (aiResponse.length > 200) {
        const sentences = aiResponse.split('. ');
        if (sentences.length > 3) {
          aiResponse = sentences.slice(0, 3).join('. ') + '.';
        }
      }
      
      return aiResponse;
    },
    
    getMockResponse(message) {
      // Mock responses for different types of questions
      const mockResponses = [
        "Kechirasiz, AI xizmati hozircha ishlamayapti. Iltimos, keyinroq urinib ko'ring yoki bizning yordam xizmatimizga murojaat qiling.",
        "Hozircha AI xizmati mavjud emas. Savolingizni @Dier_Ai telegram kanaliga yuboring, biz sizga yordam beramiz.",
        "AI xizmati vaqtincha ishlamayapti. Iltimos, biroz kutib, qaytadan urinib ko'ring.",
        "Kechirasiz, texnik xizmat ko'rsatilmoqda. Savolingizni keyinroq so'rang yoki biz bilan bog'laning.",
        "AI xizmati hozircha mavjud emas. Bizning yordam xizmatimiz sizga yordam beradi."
      ];
      
      // Random response tanlash
      const randomIndex = Math.floor(Math.random() * mockResponses.length);
      return mockResponses[randomIndex];
    },
    
    formatAIMessage(text) {
      // ** belgilarini yo'qotish
      let formattedText = text.replace(/\*\*/g, '');
      formattedText = formattedText.replace(/\*/g, '');
      
      // Boshqa formatlash belgilarini yo'qotish
      formattedText = formattedText.replace(/#/g, '');
      formattedText = formattedText.replace(/`/g, '');
      formattedText = formattedText.replace(/~/g, '');
      
      // Ortiqcha bo'shliqlarni tozalash
      formattedText = formattedText.replace(/\s+/g, ' ').trim();
      
      // Paragraflarni to'g'ri formatlash
      formattedText = formattedText.replace(/\n\n/g, '<br><br>');
      formattedText = formattedText.replace(/\n/g, '<br>');
      
      return formattedText;
    },
    scrollToBottom() {
      this.$nextTick(() => {
        const container = this.$refs.chatContainer;
        if (container) {
          const scrollElement = container.querySelector('.overflow-y-auto');
          if (scrollElement) {
            scrollElement.scrollTop = scrollElement.scrollHeight;
          }
        }
      });
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
</style>
