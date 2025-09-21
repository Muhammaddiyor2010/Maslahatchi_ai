<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <!-- Hero Section -->
      <div class="text-center mb-12 sm:mb-16 px-4">
        <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold mb-4 sm:mb-6 gradient-text animate-fade-in-down">Biz Haqimizda</h1>
        <p class="text-base sm:text-lg md:text-xl text-gray-300 max-w-3xl mx-auto leading-relaxed animate-fade-in-up animate-delay-200">
          Maslahatchi AI - sizning professional yordamchingiz barcha masalalarda
        </p>
      </div>

      <!-- Company Info -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 sm:gap-12 mb-12 sm:mb-16 px-4">
        <!-- About Text -->
        <div class="animate-slide-in-left animate-delay-300">
          <h2 class="text-2xl sm:text-3xl font-bold mb-4 sm:mb-6">Kompaniya Haqida</h2>
          <div class="space-y-3 sm:space-y-4 text-gray-300 text-sm sm:text-base">
            <p>
              Maslahatchi AI - O'zbekistondagi eng zamonaviy sun'iy intellekt texnologiyalaridan foydalanib, 
              professional maslahatlar beruvchi platforma. Biz sizning barcha sohada ehtiyojlaringizni 
              qondirish uchun ishlaymiz.
            </p>
            <p>
              Google Gemini AI texnologiyasidan foydalanib, sizga eng aniq va foydali javoblar beramiz. 
              Bizning maqsadimiz - har bir foydalanuvchiga shaxsiy maslahatchi xizmatini taqdim etish.
            </p>
            <p>
              2024-yilda tashkil etilgan bizning kompaniya qisqa vaqt ichida O'zbekistondagi eng ishonchli 
              AI maslahatchi platformasiga aylangan.
            </p>
          </div>
        </div>

        <!-- Stats -->
        <div class="grid grid-cols-2 gap-4 sm:gap-6 animate-slide-in-right animate-delay-400">
          <div v-for="(stat, index) in stats" :key="stat.label" 
               :class="'glass rounded-xl sm:rounded-2xl p-4 sm:p-6 text-center hover:scale-105 transition-transform animate-fade-in-up animate-delay-' + ((index + 5) * 100)">
            <i :class="stat.icon + ' text-2xl sm:text-3xl md:text-4xl text-primary mb-2 sm:mb-4'"></i>
            <h3 class="text-xl sm:text-2xl md:text-3xl font-bold mb-1 sm:mb-2">{{ stat.value }}</h3>
            <p class="text-gray-300 text-xs sm:text-sm">{{ stat.label }}</p>
          </div>
        </div>
      </div>

      <!-- Mission & Vision -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 sm:gap-8 mb-12 sm:mb-16 px-4">
        <div class="glass rounded-xl sm:rounded-2xl p-6 sm:p-8 animate-slide-in-left animate-delay-800">
          <div class="text-center mb-4 sm:mb-6">
            <i class="fas fa-bullseye text-3xl sm:text-4xl md:text-5xl text-primary mb-3 sm:mb-4"></i>
            <h3 class="text-xl sm:text-2xl font-bold">Bizning Maqsad</h3>
          </div>
          <p class="text-gray-300 text-center text-sm sm:text-base">
            Har bir foydalanuvchiga eng sifatli va professional maslahatlar berish orqali 
            ularning muvaffaqiyatiga yordam berish. Zamonaviy AI texnologiyalaridan foydalanib, 
            bilim va tajriba bo'yicha teng imkoniyatlar yaratish.
          </p>
        </div>

        <div class="glass rounded-xl sm:rounded-2xl p-6 sm:p-8 animate-slide-in-right animate-delay-900">
          <div class="text-center mb-4 sm:mb-6">
            <i class="fas fa-eye text-3xl sm:text-4xl md:text-5xl text-secondary mb-3 sm:mb-4"></i>
            <h3 class="text-xl sm:text-2xl font-bold">Bizning Vizyon</h3>
          </div>
          <p class="text-gray-300 text-center text-sm sm:text-base">
            O'zbekistonda va butun Markaziy Osiyoda eng katta va eng ishonchli 
            AI maslahatchi platformasiga aylanish. Har bir odam uchun professional 
            yordam olish imkoniyatini yaratish.
          </p>
        </div>
      </div>

      <!-- Contact Information & Form -->
      <div class="mb-12 sm:mb-16 px-4">
        <h2 class="text-2xl sm:text-3xl font-bold text-center mb-8 sm:mb-12 animate-fade-in-up animate-delay-1000">Biz bilan bog'laning</h2>
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 sm:gap-12">
          <!-- Contact Info -->
          <div class="animate-slide-in-left animate-delay-1100">
            <h3 class="text-xl sm:text-2xl font-bold mb-6 sm:mb-8">Aloqa Ma'lumotlari</h3>
            <div class="space-y-4 sm:space-y-6">
              <div v-for="(contact, index) in contacts" :key="contact.title" 
                   :class="'glass rounded-lg p-4 sm:p-6 hover:scale-105 transition-all duration-300 animate-fade-in-up animate-delay-' + ((index + 12) * 100)">
                <div class="flex items-center">
                  <i :class="contact.icon + ' ' + contact.color" class="text-xl sm:text-2xl mr-3 sm:mr-4"></i>
                  <div>
                    <h4 class="font-semibold text-sm sm:text-base">{{ contact.title }}</h4>
                    <a :href="contact.link" :class="contact.color" 
                       class="hover:underline text-sm sm:text-base">{{ contact.value }}</a>
                  </div>
                </div>
              </div>
            </div>

            <!-- Quick Contact -->
            <div class="mt-6 sm:mt-8 text-center">
              <p class="text-gray-300 mb-3 sm:mb-4 text-sm sm:text-base">Tezkor yordam kerakmi?</p>
              <a href="https://t.me/Dier_Ai" target="_blank" 
                 class="inline-flex items-center bg-blue-600 hover:bg-blue-700 px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-semibold transition-colors text-sm sm:text-base">
                <i class="fab fa-telegram mr-2"></i>Telegram orqali yozing
              </a>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="animate-slide-in-right animate-delay-1200">
            <h3 class="text-xl sm:text-2xl font-bold mb-6 sm:mb-8">Xabar Yuborish</h3>
            <div class="glass rounded-lg p-6 sm:p-8">
              <form @submit.prevent="submitForm" class="space-y-4 sm:space-y-6">
                <div>
                  <label class="block text-sm font-medium mb-2">Ismingiz *</label>
                  <input v-model="form.name" type="text" required
                         class="w-full bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-3 sm:px-4 py-2 sm:py-3 text-white dark:text-white light:text-gray-900 focus:border-primary focus:outline-none text-sm sm:text-base">
                </div>
                <div>
                  <label class="block text-sm font-medium mb-2">Email *</label>
                  <input v-model="form.email" type="email" required
                         class="w-full bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-3 sm:px-4 py-2 sm:py-3 text-white dark:text-white light:text-gray-900 focus:border-primary focus:outline-none text-sm sm:text-base">
                </div>
                <div>
                  <label class="block text-sm font-medium mb-2">Xabar *</label>
                  <textarea v-model="form.message" rows="4" required
                            class="w-full bg-gray-800 dark:bg-gray-800 light:bg-white border border-gray-600 dark:border-gray-600 light:border-gray-300 rounded-lg px-3 sm:px-4 py-2 sm:py-3 text-white dark:text-white light:text-gray-900 focus:border-primary focus:outline-none text-sm sm:text-base"></textarea>
                </div>
                <button type="submit" 
                        class="w-full bg-gradient-to-r from-primary to-secondary py-2 sm:py-3 rounded-lg font-semibold hover:scale-105 transition-transform text-sm sm:text-base">
                  <i class="fas fa-paper-plane mr-2"></i>Xabar Yuborish
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Map Section -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-8">Bizning Joylashuvimiz</h2>
        <div class="glass rounded-2xl p-8">
          <div class="text-center mb-6">
            <i class="fas fa-map text-5xl text-primary mb-4"></i>
            <h3 class="text-2xl font-bold mb-2">Qo'qon, O'zbekiston</h3>
            <p class="text-gray-300">Bizning ofis Qo'qon shahrida joylashgan</p>
          </div>
          
          <!-- Map Section -->
          <div class="bg-gray-800 rounded-lg p-8">
            <div class="text-center mb-6">
              <i class="fas fa-map-marker-alt text-6xl text-primary mb-4"></i>
              <h3 class="text-2xl font-bold mb-2">Qo'qon, O'zbekiston</h3>
              <p class="text-gray-300 mb-6">Bizning ofis Qo'qon shahrida joylashgan</p>
            </div>
            
            <!-- Map Embed -->
            <div class="bg-gray-700 rounded-lg overflow-hidden mb-6">
              <iframe 
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3010.123456789!2d71.005388!3d40.518417!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zNDDCsDMxJzA2LjMiTiA3McKwMDAnMTkuNCJF!5e0!3m2!1suz!2s!4v1234567890123!5m2!1suz!2s"
                width="100%" 
                height="300" 
                style="border:0;" 
                allowfullscreen="" 
                loading="lazy" 
                referrerpolicy="no-referrer-when-downgrade">
              </iframe>
            </div>
            
            <!-- Alternative Map Links -->
            <div class="text-center">
              <p class="text-gray-300 mb-4">Xaritada to'liq ko'rish uchun:</p>
              <div class="flex flex-col sm:flex-row gap-4 justify-center">
                <a href="https://www.google.com/maps/search/?api=1&query=40.518417,71.005388" 
                   target="_blank"
                   class="inline-flex items-center bg-primary hover:bg-primary/80 px-6 py-3 rounded-lg font-semibold transition-colors">
                  <i class="fab fa-google mr-2"></i>
                  Google Xaritada Ko'rish
                </a>
                <a href="https://yandex.uz/maps/geo/1939283421/?ll=71.005388%2C40.518417&utm_campaign=desktop&utm_medium=search&utm_source=maps&z=17.92" 
                   target="_blank"
                   class="inline-flex items-center bg-yellow-600 hover:bg-yellow-700 px-6 py-3 rounded-lg font-semibold transition-colors">
                  <i class="fas fa-map mr-2"></i>
                  Yandex Xaritada Ko'rish
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Team Section -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Bizning Jamoa</h2>
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="member in team" :key="member.name" 
               class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform">
            <div class="w-24 h-24 bg-gradient-to-br from-primary to-secondary rounded-full mx-auto mb-4 flex items-center justify-center">
              <i :class="member.icon + ' text-2xl text-white'"></i>
            </div>
            <h3 class="text-xl font-bold mb-2">{{ member.name }}</h3>
            <p class="text-primary mb-3">{{ member.position }}</p>
            <p class="text-gray-300 text-sm">{{ member.description }}</p>
            <div class="flex justify-center space-x-3 mt-4">
              <a v-if="member.telegram" :href="member.telegram" target="_blank" 
                 class="text-blue-400 hover:text-blue-300">
                <i class="fab fa-telegram text-xl"></i>
              </a>
              <a v-if="member.email" :href="'mailto:' + member.email" 
                 class="text-red-400 hover:text-red-300">
                <i class="fas fa-envelope text-xl"></i>
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- Values -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Bizning Qadriyatlar</h2>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div v-for="value in values" :key="value.title" 
               class="glass rounded-lg p-6 text-center">
            <i :class="value.icon + ' text-3xl text-primary mb-4'"></i>
            <h3 class="text-lg font-bold mb-2">{{ value.title }}</h3>
            <p class="text-gray-300 text-sm">{{ value.description }}</p>
          </div>
        </div>
      </div>

      <!-- Additional Information -->
      <div class="mb-16">
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
      <div class="mb-16">
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

      <!-- CTA Section -->
      <div class="text-center">
        <div class="glass rounded-2xl p-12">
          <h2 class="text-3xl font-bold mb-4">Bizga Qo'shiling!</h2>
          <p class="text-xl text-gray-300 mb-8 max-w-2xl mx-auto">
            Professional AI maslahatlardan foydalanishni boshlang va o'z muvaffaqiyatingizni 
            yangi darajaga ko'taring.
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <router-link to="/" 
                         class="bg-gradient-to-r from-primary to-secondary px-8 py-4 rounded-lg text-lg font-semibold hover:scale-105 transition-transform">
              <i class="fas fa-play mr-2"></i>Bepul Boshlash
            </router-link>
            <router-link to="/pricing" 
                         class="border-2 border-primary px-8 py-4 rounded-lg text-lg font-semibold hover:bg-primary/10 transition-colors">
              Narxlarni Ko'rish
            </router-link>
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
  name: 'About',
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
      ],
      stats: [
        { icon: 'fas fa-users', value: '10,000+', label: 'Foydalanuvchilar' },
        { icon: 'fas fa-comments', value: '50,000+', label: 'Maslahatlar' },
        { icon: 'fas fa-star', value: '4.9/5', label: 'Reyting' },
        { icon: 'fas fa-clock', value: '24/7', label: 'Yordam' }
      ],
      team: [
        {
          name: 'Muhammaddiyorjon',
          position: 'Asoschisi & CEO',
          description: 'AI texnologiyalari va biznes strategiyasi bo\'yicha mutaxassis',
          icon: 'fas fa-user-tie',
          telegram: 'https://t.me/Dier_Ai',
          email: 'Muhammaddiyorjon2010@icloud.com'
        },
        {
          name: 'AI Texnologiya Jamoasi',
          position: 'Rivojlanish',
          description: 'Gemini AI integratsiyasi va texnik yechimlar',
          icon: 'fas fa-code',
          telegram: null,
          email: null
        },
        {
          name: 'Qo\'llab-quvvatlash Jamoasi',
          position: 'Mijozlar Xizmati',
          description: '24/7 professional yordam va maslahatlar',
          icon: 'fas fa-headset',
          telegram: 'https://t.me/Dier_Ai',
          email: 'Muhammaddiyorjon2010@icloud.com'
        }
      ],
      values: [
        {
          icon: 'fas fa-shield-alt',
          title: 'Ishonchlilik',
          description: 'Barcha ma\'lumotlaringiz xavfsiz va maxfiy'
        },
        {
          icon: 'fas fa-rocket',
          title: 'Innovatsiya',
          description: 'Eng zamonaviy AI texnologiyalaridan foydalanish'
        },
        {
          icon: 'fas fa-heart',
          title: 'Sifat',
          description: 'Eng yuqori sifatli maslahatlar va xizmatlar'
        },
        {
          icon: 'fas fa-users',
          title: 'Jamoa',
          description: 'Professional mutaxassislar jamoasi'
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