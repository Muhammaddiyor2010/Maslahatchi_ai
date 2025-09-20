<template>
  <div v-if="show" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50">
    <div class="glass rounded-2xl p-8 max-w-lg w-full mx-4">
      <div class="text-center mb-6">
        <i class="fas fa-key text-4xl text-primary mb-4"></i>
        <h3 class="text-2xl font-bold mb-2">Token Kodni Kiriting</h3>
        <p class="text-gray-300">{{ plan.toUpperCase() }} rejimini faollashtirish uchun token kodingizni kiriting.</p>
      </div>
      
      <div class="mb-6">
        <label class="block text-sm font-medium mb-2">Token Kod</label>
        <input v-model="tokenCode" 
               placeholder="Token kodingizni kiriting..." 
               @keyup.enter="verifyToken"
               :class="[
                 'w-full bg-gray-800 dark:bg-gray-800 light:bg-white border rounded-lg px-4 py-3 text-white dark:text-white light:text-gray-900 focus:outline-none',
                 error ? 'border-red-500' : success ? 'border-green-500' : 'border-gray-600 dark:border-gray-600 light:border-gray-300 focus:border-primary'
               ]">
        
        <!-- Error Message -->
        <div v-if="error" class="mt-2 p-3 bg-red-900/50 border border-red-500 rounded-lg">
          <div class="flex items-center">
            <i class="fas fa-exclamation-triangle text-red-400 mr-2"></i>
            <span class="text-red-300 text-sm">{{ error }}</span>
          </div>
        </div>
        
        <!-- Success Message -->
        <div v-if="success" class="mt-2 p-3 bg-green-900/50 border border-green-500 rounded-lg">
          <div class="flex items-center">
            <i class="fas fa-check-circle text-green-400 mr-2"></i>
            <span class="text-green-300 text-sm">{{ success }}</span>
          </div>
        </div>
      </div>

      <!-- Token Examples -->
      <div class="mb-6">
        <p class="text-sm font-medium mb-3">Test Token Kodlari:</p>
        <div class="grid grid-cols-2 gap-2">
          <button v-if="plan === 'pro'" 
                  @click="tokenCode = 'pro123'" 
                  class="text-xs bg-gray-700 hover:bg-gray-600 px-3 py-2 rounded text-left">
            pro123
          </button>
          <button v-if="plan === 'pro'" 
                  @click="tokenCode = 'pro456'" 
                  class="text-xs bg-gray-700 hover:bg-gray-600 px-3 py-2 rounded text-left">
            pro456
          </button>
          <button v-if="plan === 'advanced'" 
                  @click="tokenCode = 'adv123'" 
                  class="text-xs bg-gray-700 hover:bg-gray-600 px-3 py-2 rounded text-left">
            adv123
          </button>
          <button v-if="plan === 'advanced'" 
                  @click="tokenCode = 'adv456'" 
                  class="text-xs bg-gray-700 hover:bg-gray-600 px-3 py-2 rounded text-left">
            adv456
          </button>
        </div>
      </div>

      <div class="flex gap-3 mb-4">
        <button @click="verifyToken" 
                :disabled="!tokenCode.trim()"
                class="flex-1 bg-primary hover:bg-primary/80 disabled:opacity-50 px-4 py-3 rounded-lg font-semibold transition-colors">
          <i class="fas fa-check mr-2"></i>Tasdiqlash
        </button>
        <button @click="closeModal" 
                class="flex-1 bg-gray-700 hover:bg-gray-600 px-4 py-3 rounded-lg font-semibold transition-colors">
          <i class="fas fa-times mr-2"></i>Bekor qilish
        </button>
      </div>

      <div class="text-center">
        <p class="text-sm text-gray-400 mb-2">Token kodi yo'qmi?</p>
        <button @click="contactTelegram" class="text-primary hover:underline flex items-center justify-center mx-auto">
          <i class="fab fa-telegram mr-2"></i>@Dier_Ai ga murojaat qiling
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TokenModal',
  props: {
    show: {
      type: Boolean,
      default: false
    },
    plan: {
      type: String,
      default: 'pro'
    }
  },
  emits: ['close', 'success'],
  data() {
    return {
      tokenCode: '',
      error: '',
      success: ''
    }
  },
  methods: {
    verifyToken() {
      // Clear previous messages
      this.error = '';
      this.success = '';
      
      if (!this.tokenCode.trim()) {
        this.error = 'Token kodni kiriting!';
        return;
      }
      
      // Simple token validation (in real app, this would be server-side)
      const validTokens = {
        'pro': ['pro123', 'pro456', 'pro789'],
        'advanced': ['adv123', 'adv456', 'adv789']
      };
      
      if (validTokens[this.plan] && validTokens[this.plan].includes(this.tokenCode)) {
        this.success = `${this.plan.toUpperCase()} rejim muvaffaqiyatli faollashtirildi!`;
        
        setTimeout(() => {
          this.$emit('success', this.plan);
          this.closeModal();
        }, 1500);
      } else {
        this.error = 'Noto\'g\'ri token kod! Iltimos, to\'g\'ri kodni kiriting.';
        setTimeout(() => {
          this.error = '';
        }, 3000);
      }
    },
    closeModal() {
      this.tokenCode = '';
      this.error = '';
      this.success = '';
      this.$emit('close');
    },
    contactTelegram() {
      window.open('https://t.me/Dier_Ai', '_blank');
    }
  },
  watch: {
    show(newVal) {
      if (newVal) {
        this.tokenCode = '';
        this.error = '';
        this.success = '';
      }
    }
  }
}
</script>

<style scoped>
.text-primary {
  color: #6366f1;
}
</style>
