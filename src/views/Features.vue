<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16">
        <h1 class="text-4xl md:text-6xl font-bold mb-6 gradient-text">Xususiyatlar</h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          Maslahatchi AI sizga eng zamonaviy texnologiyalar orqali yordam beradi
        </p>
      </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="feature in features" :key="feature.title" 
             class="glass rounded-2xl p-6 hover:scale-105 transition-all duration-300 animate-float">
          <i :class="feature.icon + ' ' + feature.color" class="text-4xl mb-4"></i>
          <h3 class="text-xl font-bold mb-3">{{ feature.title }}</h3>
          <p class="text-gray-300">{{ feature.description }}</p>
        </div>
      </div>

      <!-- Demo Video Section -->
      <div class="mt-20 text-center">
        <h2 class="text-3xl font-bold mb-8">Qanday Ishlaydi</h2>
        <div class="glass rounded-2xl p-8 max-w-4xl mx-auto">
          <div class="bg-gray-800 rounded-lg h-64 flex items-center justify-center mb-6">
            <div class="text-center">
              <i class="fas fa-play-circle text-6xl text-primary mb-4"></i>
              <p class="text-gray-300">Demo Video Ko'rish</p>
            </div>
          </div>
          <div class="grid md:grid-cols-3 gap-6 text-sm">
            <div class="text-center">
              <div class="bg-primary w-8 h-8 rounded-full flex items-center justify-center mx-auto mb-2">1</div>
              <p>Savolingizni yozing</p>
            </div>
            <div class="text-center">
              <div class="bg-secondary w-8 h-8 rounded-full flex items-center justify-center mx-auto mb-2">2</div>
              <p>AI tahlil qiladi</p>
            </div>
            <div class="text-center">
              <div class="bg-green-500 w-8 h-8 rounded-full flex items-center justify-center mx-auto mb-2">3</div>
              <p>Javob olasiz</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Features Details -->
      <div class="mt-20">
        <h2 class="text-3xl font-bold text-center mb-12">Batafsil Xususiyatlar</h2>
        <div class="grid md:grid-cols-2 gap-8">
          <div class="glass rounded-lg p-6">
            <h3 class="text-xl font-bold mb-4 text-primary">AI Texnologiyasi</h3>
            <p class="text-gray-300 mb-4">
              Eng zamonaviy sun'iy intellekt texnologiyalaridan foydalanib, 
              sizning savollaringizga aniq va foydali javoblar beramiz.
            </p>
            <ul class="space-y-2 text-gray-300">
              <li><i class="fas fa-check text-green-400 mr-2"></i>GPT-4 texnologiyasi</li>
              <li><i class="fas fa-check text-green-400 mr-2"></i>Tabiiy tilni tushunish</li>
              <li><i class="fas fa-check text-green-400 mr-2"></i>Kontekstual javoblar</li>
            </ul>
          </div>
          
          <div class="glass rounded-lg p-6">
            <h3 class="text-xl font-bold mb-4 text-primary">Professional Yordam</h3>
            <p class="text-gray-300 mb-4">
              Har bir maslahat professional mutaxassislar tomonidan 
              tekshiriladi va sizning ehtiyojlaringizga moslashtiriladi.
            </p>
            <ul class="space-y-2 text-gray-300">
              <li><i class="fas fa-check text-green-400 mr-2"></i>Ekspert darajasida maslahat</li>
              <li><i class="fas fa-check text-green-400 mr-2"></i>Shaxsiylashtirilgan yondashuv</li>
              <li><i class="fas fa-check text-green-400 mr-2"></i>Doimiy kuzatuv</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Features',
  data() {
    return {
      features: [
        {
          icon: 'fas fa-brain',
          title: 'Aqlli Tahlil',
          description: 'AI texnologiyasi orqali chuqur tahlil va aniq javoblar',
          color: 'text-blue-400'
        },
        {
          icon: 'fas fa-rocket',
          title: 'Tezkor Javoblar',
          description: 'Bir necha soniyada professional maslahatlar olish',
          color: 'text-green-400'
        },
        {
          icon: 'fas fa-shield-alt',
          title: 'Xavfsizlik',
          description: 'Barcha ma\'lumotlaringiz himoyalangan va maxfiy',
          color: 'text-red-400'
        },
        {
          icon: 'fas fa-globe',
          title: '24/7 Mavjudlik',
          description: 'Har qanday vaqtda, istalgan joydan foydalaning',
          color: 'text-purple-400'
        },
        {
          icon: 'fas fa-chart-line',
          title: 'Taraqqiyot Kuzatuvi',
          description: 'Sizning rivojlanishingizni kuzatib boring',
          color: 'text-yellow-400'
        },
        {
          icon: 'fas fa-users',
          title: 'Jamoa Yordami',
          description: 'Professional mutaxassislar jamoasi sizga yordam beradi',
          color: 'text-indigo-400'
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
