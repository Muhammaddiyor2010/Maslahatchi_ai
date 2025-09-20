<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16">
        <h1 class="text-4xl md:text-6xl font-bold mb-6 gradient-text">Aloqa</h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          Bizga murojaat qiling va professional AI maslahatlardan foydalaning. 
          Har qanday savol yoki taklif uchun biz bilan bog'laning.
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
            <div class="bg-gray-800 rounded-lg overflow-hidden h-64">
              <iframe 
                src="https://yandex.uz/maps/geo/1939283421/?ll=71.005388%2C40.518417&utm_campaign=desktop&utm_medium=search&utm_source=maps&z=17.92"
                width="100%" 
                height="100%" 
                style="border:0;" 
                allowfullscreen="" 
                loading="lazy" 
                referrerpolicy="no-referrer-when-downgrade">
              </iframe>
            </div>
            <div class="mt-4 text-center">
              <a href="https://yandex.uz/maps/geo/1939283421/?ll=71.005388%2C40.518417&utm_campaign=desktop&utm_medium=search&utm_source=maps&z=17.92" 
                 target="_blank"
                 class="inline-flex items-center text-primary hover:underline">
                <i class="fas fa-external-link-alt mr-2"></i>
                Yandex Xaritada Ko'rish
              </a>
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

      <!-- Additional Information -->
      <div class="mt-16">
        <h2 class="text-3xl font-bold text-center mb-12">Qo'shimcha Ma'lumotlar</h2>
        <div class="grid md:grid-cols-3 gap-8">
          <!-- Working Hours -->
          <div class="glass rounded-2xl p-6 text-center">
            <i class="fas fa-clock text-4xl text-primary mb-4"></i>
            <h3 class="text-xl font-bold mb-3">Ish Vaqtlari</h3>
            <div class="space-y-2 text-gray-300">
              <p><strong>Dushanba - Juma:</strong> 9:00 - 18:00</p>
              <p><strong>Shanba:</strong> 10:00 - 16:00</p>
              <p><strong>Yakshanba:</strong> Dam olish</p>
            </div>
          </div>

          <!-- Response Time -->
          <div class="glass rounded-2xl p-6 text-center">
            <i class="fas fa-reply text-4xl text-green-400 mb-4"></i>
            <h3 class="text-xl font-bold mb-3">Javob Vaqti</h3>
            <div class="space-y-2 text-gray-300">
              <p><strong>Email:</strong> 24 soat ichida</p>
              <p><strong>Telegram:</strong> 2 soat ichida</p>
              <p><strong>Telefon:</strong> Darhol</p>
            </div>
          </div>

          <!-- Languages -->
          <div class="glass rounded-2xl p-6 text-center">
            <i class="fas fa-language text-4xl text-blue-400 mb-4"></i>
            <h3 class="text-xl font-bold mb-3">Tillar</h3>
            <div class="space-y-2 text-gray-300">
              <p><strong>O'zbek:</strong> Asosiy</p>
              <p><strong>Rus:</strong> Qo'llab-quvvatlanadi</p>
              <p><strong>Ingliz:</strong> Qo'llab-quvvatlanadi</p>
            </div>
          </div>
        </div>
      </div>

      <!-- FAQ Section -->
      <div class="mt-16">
        <h2 class="text-3xl font-bold text-center mb-12">Tez-tez So'raladigan Savollar</h2>
        <div class="max-w-4xl mx-auto space-y-6">
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2 text-primary">Qanday qilib siz bilan bog'lanish mumkin?</h3>
            <p class="text-gray-300">Biz bilan email, telefon yoki Telegram orqali bog'lanishingiz mumkin. Barcha usullar 24/7 mavjud.</p>
          </div>
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2 text-primary">Javob qachon keladi?</h3>
            <p class="text-gray-300">Email orqali 24 soat ichida, Telegram orqali 2 soat ichida, telefon orqali esa darhol javob beramiz.</p>
          </div>
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2 text-primary">Qanday tillarda yozish mumkin?</h3>
            <p class="text-gray-300">Siz o'zbek, rus yoki ingliz tillarida yozishingiz mumkin. Biz barcha tillarda professional javob beramiz.</p>
          </div>
          <div class="glass rounded-lg p-6">
            <h3 class="font-semibold mb-2 text-primary">Ofisimizga kelish mumkinmi?</h3>
            <p class="text-gray-300">Ha, albatta! Bizning ofisimiz Qo'qon shahrida joylashgan. Kelishdan oldin telefon qilib ma'lum qilish tavsiya etiladi.</p>
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
          value: 'Muhammaddiyorjon2010@icloud.com',
          link: 'mailto:Muhammaddiyorjon2010@icloud.com',
          color: 'text-red-400'
        },
        {
          icon: 'fas fa-phone',
          title: 'Telefon',
          value: '+998 93 198 17 93',
          link: 'tel:+998931981793',
          color: 'text-green-400'
        },
        {
          icon: 'fas fa-map-marker-alt',
          title: 'Manzil',
          value: 'Qo\'qon, O\'zbekiston',
          link: 'https://yandex.uz/maps/geo/1939283421/?ll=71.005388%2C40.518417&utm_campaign=desktop&utm_medium=search&utm_source=maps&z=17.92',
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