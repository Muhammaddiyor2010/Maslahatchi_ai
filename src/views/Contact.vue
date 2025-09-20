<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16">
        <h1 class="text-4xl md:text-6xl font-bold mb-6 gradient-text">Aloqa</h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          Bizga murojaat qiling va professional yordam oling
        </p>
      </div>

      <div class="grid lg:grid-cols-2 gap-12">
        <!-- Contact Info -->
        <div>
          <h2 class="text-2xl font-bold mb-8">Biz bilan bog'laning</h2>
          <div class="space-y-6">
            <div v-for="contact in contacts" :key="contact.title" 
                 class="glass rounded-lg p-6 hover:scale-105 transition-all duration-300">
              <div class="flex items-center">
                <i :class="contact.icon + ' ' + contact.color" class="text-2xl mr-4"></i>
                <div>
                  <h3 class="font-semibold">{{ contact.title }}</h3>
                  <a :href="contact.link" :class="contact.color" 
                     class="hover:underline">{{ contact.value }}</a>
                </div>
              </div>
            </div>
          </div>

          <!-- Map -->
          <div class="glass rounded-lg p-6 mt-8">
            <h3 class="font-semibold mb-4">Bizning joylashuvimiz</h3>
            <div class="bg-gray-800 rounded-lg h-48 flex items-center justify-center">
              <div class="text-center">
                <i class="fas fa-map text-4xl text-primary mb-2"></i>
                <p class="text-gray-300">Xarita bu yerda bo'ladi</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Contact Form -->
        <div>
          <h2 class="text-2xl font-bold mb-8">Xabar Yuborish</h2>
          <div class="glass rounded-lg p-8">
            <form @submit.prevent="submitForm" class="space-y-6">
              <div>
                <label class="block text-sm font-medium mb-2">Ismingiz *</label>
              <input v-model="form.name" type="text" required
                     class="w-full bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-4 py-3 text-white dark:text-white light:text-gray-900 focus:border-primary focus:outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium mb-2">Email *</label>
                <input v-model="form.email" type="email" required
                       class="w-full bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-4 py-3 text-white dark:text-white light:text-gray-900 focus:border-primary focus:outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium mb-2">Xabar *</label>
                <textarea v-model="form.message" rows="5" required
                          class="w-full bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-4 py-3 text-white dark:text-white light:text-gray-900 focus:border-primary focus:outline-none"></textarea>
              </div>
              <button type="submit" 
                      class="w-full bg-gradient-to-r from-primary to-secondary py-3 rounded-lg font-semibold hover:scale-105 transition-transform">
                <i class="fas fa-paper-plane mr-2"></i>Xabar Yuborish
              </button>
            </form>
          </div>

          <!-- Quick Contact -->
          <div class="mt-8 text-center">
            <p class="text-gray-300 mb-4">Tezkor yordam kerakmi?</p>
            <a href="https://t.me/Dier_Ai" target="_blank" 
               class="inline-flex items-center bg-blue-600 hover:bg-blue-700 px-6 py-3 rounded-lg font-semibold transition-colors">
              <i class="fab fa-telegram mr-2"></i>Telegram orqali yozing
            </a>
          </div>
        </div>
      </div>

      <!-- Success Message -->
      <div v-if="submitted" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50">
        <div class="glass rounded-2xl p-8 max-w-md w-full mx-4 text-center">
          <i class="fas fa-check-circle text-6xl text-green-400 mb-4"></i>
          <h3 class="text-2xl font-bold mb-4">Xabar Yuborildi!</h3>
          <p class="text-gray-300 mb-6">Sizning xabaringiz muvaffaqiyatli yuborildi. Tez orada javob beramiz.</p>
          <button @click="submitted = false" class="bg-primary px-6 py-3 rounded-lg font-semibold">
            Yopish
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      form: {
        name: '',
        email: '',
        message: ''
      },
      submitted: false,
      contacts: [
        {
          icon: 'fab fa-telegram',
          title: 'Telegram',
          value: '@Dier_Ai',
          link: 'https://t.me/Dier_Ai',
          color: 'text-blue-400'
        },
        {
          icon: 'fas fa-envelope',
          title: 'Email',
          value: 'info@maslahatchi.ai',
          link: 'mailto:info@maslahatchi.ai',
          color: 'text-red-400'
        },
        {
          icon: 'fas fa-phone',
          title: 'Telefon',
          value: '+998 90 123 45 67',
          link: 'tel:+998901234567',
          color: 'text-green-400'
        },
        {
          icon: 'fas fa-map-marker-alt',
          title: 'Manzil',
          value: 'Toshkent, O\'zbekiston',
          link: '#',
          color: 'text-yellow-400'
        }
      ]
    }
  },
  methods: {
    submitForm() {
      if (this.form.name && this.form.email && this.form.message) {
        this.submitted = true;
        this.form = { name: '', email: '', message: '' };
        
        // Hide success message after 5 seconds
        setTimeout(() => {
          this.submitted = false;
        }, 5000);
      } else {
        alert('Iltimos, barcha maydonlarni to\'ldiring!');
      }
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