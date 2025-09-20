<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <!-- Hero Section -->
      <div class="text-center mb-16">
        <h1 class="text-4xl md:text-6xl font-bold mb-6 gradient-text">Biz Haqimizda</h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          Maslahatchi AI - sizning professional yordamchingiz barcha masalalarda
        </p>
      </div>

      <!-- Company Info -->
      <div class="grid lg:grid-cols-2 gap-12 mb-16">
        <!-- About Text -->
        <div>
          <h2 class="text-3xl font-bold mb-6">Kompaniya Haqida</h2>
          <div class="space-y-4 text-gray-300">
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
        <div class="grid grid-cols-2 gap-6">
          <div v-for="stat in stats" :key="stat.label" 
               class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform">
            <i :class="stat.icon + ' text-4xl text-primary mb-4'"></i>
            <h3 class="text-3xl font-bold mb-2">{{ stat.value }}</h3>
            <p class="text-gray-300">{{ stat.label }}</p>
          </div>
        </div>
      </div>

      <!-- Mission & Vision -->
      <div class="grid md:grid-cols-2 gap-8 mb-16">
        <div class="glass rounded-2xl p-8">
          <div class="text-center mb-6">
            <i class="fas fa-bullseye text-5xl text-primary mb-4"></i>
            <h3 class="text-2xl font-bold">Bizning Maqsad</h3>
          </div>
          <p class="text-gray-300 text-center">
            Har bir foydalanuvchiga eng sifatli va professional maslahatlar berish orqali 
            ularning muvaffaqiyatiga yordam berish. Zamonaviy AI texnologiyalaridan foydalanib, 
            bilim va tajriba bo'yicha teng imkoniyatlar yaratish.
          </p>
        </div>

        <div class="glass rounded-2xl p-8">
          <div class="text-center mb-6">
            <i class="fas fa-eye text-5xl text-secondary mb-4"></i>
            <h3 class="text-2xl font-bold">Bizning Vizyon</h3>
          </div>
          <p class="text-gray-300 text-center">
            O'zbekistonda va butun Markaziy Osiyoda eng katta va eng ishonchli 
            AI maslahatchi platformasiga aylanish. Har bir odam uchun professional 
            yordam olish imkoniyatini yaratish.
          </p>
        </div>
      </div>

      <!-- Contact Information -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Aloqa Ma'lumotlari</h2>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <!-- Email -->
          <div class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform">
            <i class="fas fa-envelope text-4xl text-red-400 mb-4"></i>
            <h3 class="text-lg font-semibold mb-2">Email</h3>
            <a href="mailto:Muhammaddiyorjon2010@icloud.com" 
               class="text-primary hover:underline break-all">
              Muhammaddiyorjon2010@icloud.com
            </a>
          </div>

          <!-- Phone -->
          <div class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform">
            <i class="fas fa-phone text-4xl text-green-400 mb-4"></i>
            <h3 class="text-lg font-semibold mb-2">Telefon</h3>
            <a href="tel:+998931981793" 
               class="text-primary hover:underline">
              +998 93 198 17 93
            </a>
          </div>

          <!-- Location -->
          <div class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform">
            <i class="fas fa-map-marker-alt text-4xl text-yellow-400 mb-4"></i>
            <h3 class="text-lg font-semibold mb-2">Manzil</h3>
            <p class="text-gray-300">Qo'qon, O'zbekiston</p>
          </div>

          <!-- Telegram -->
          <div class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform">
            <i class="fab fa-telegram text-4xl text-blue-400 mb-4"></i>
            <h3 class="text-lg font-semibold mb-2">Telegram</h3>
            <a href="https://t.me/Dier_Ai" target="_blank" 
               class="text-primary hover:underline">
              @Dier_Ai
            </a>
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
          
          <!-- Map Embed -->
          <div class="bg-gray-800 rounded-lg overflow-hidden">
            <iframe 
              src="https://yandex.uz/maps/geo/1939283421/?ll=71.005388%2C40.518417&utm_campaign=desktop&utm_medium=search&utm_source=maps&z=17.92"
              width="100%" 
              height="400" 
              style="border:0;" 
              allowfullscreen="" 
              loading="lazy" 
              referrerpolicy="no-referrer-when-downgrade">
            </iframe>
          </div>
          
          <div class="mt-4 text-center">
            <a href="https://yandex.uz/maps/geo/1939283421/?ll=71.005388%2C40.518417&utm_campaign=desktop&utm_medium=search&utm_source=maps&z=17.92" 
               target="_blank"
               class="inline-flex items-center bg-primary hover:bg-primary/80 px-6 py-3 rounded-lg font-semibold transition-colors">
              <i class="fas fa-external-link-alt mr-2"></i>
              Yandex Xaritada Ko'rish
            </a>
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'About',
  data() {
    return {
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