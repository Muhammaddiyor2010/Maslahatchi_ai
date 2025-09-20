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
                <li><i class="fas fa-times text-red-400 mr-2"></i>AI maslahatchi yo'q</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Sayt ko'rish</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Rejimlar haqida ma'lumot</li>
              </ul>
              <div class="mt-4">
                <span class="text-xs text-red-400">AI ishlamaydi</span>
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

        <!-- Default Advice for Free Plan -->
        <div v-if="currentPlan === 'free'" class="max-w-4xl mx-auto mb-16">
          <h2 class="text-3xl font-bold text-center mb-8">Foydali Maslahatlar</h2>
          <div class="grid md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-lightbulb text-4xl text-yellow-400 mb-3"></i>
                <h3 class="text-xl font-bold text-yellow-400">Ishda Muvaffaqiyat</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Maqsadlaringizni aniq belgilang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Vaqtingizni to'g'ri boshqaring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Doimiy o'rganish jarayonini davom eting</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Jamoa bilan yaxshi hamkorlik qiling</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-heart text-4xl text-red-400 mb-3"></i>
                <h3 class="text-xl font-bold text-red-400">Sog'liq</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Muntazam jismoniy mashqlar</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>To'g'ri ovqatlanish</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Yetarli uxlash</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Stress bilan kurashish</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-graduation-cap text-4xl text-blue-400 mb-3"></i>
                <h3 class="text-xl font-bold text-blue-400">Ta'lim</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Kunlik o'qish odatini shakllantiring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Amaliy bilimlarni qo'llang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Turli manbalardan o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Bilimlaringizni boshqalar bilan baham ko'ring</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-users text-4xl text-green-400 mb-3"></i>
                <h3 class="text-xl font-bold text-green-400">Ijtimoiy Hayot</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Oilangizga vaqt ajrating</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Do'stlar bilan aloqani saqlang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Yangi odamlar bilan tanishing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Ijtimoiy faoliyatda qatnashing</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-coins text-4xl text-yellow-500 mb-3"></i>
                <h3 class="text-xl font-bold text-yellow-500">Moliyaviy Maslahat</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Har oy jamg'arma qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Moliyaviy reja tuzing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Keraksiz xarajatlarni kamaytiring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Investitsiya haqida o'rganing</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-rocket text-4xl text-purple-400 mb-3"></i>
                <h3 class="text-xl font-bold text-purple-400">Rivojlanish</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Shaxsiy rivojlanish rejasi</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Yangiliklarga ochiq bo'ling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Xatolardan o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Professional yordam so'rang</li>
              </ul>
            </div>

            <!-- Yangi Maslahatlar -->
            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-brain text-4xl text-indigo-400 mb-3"></i>
                <h3 class="text-xl font-bold text-indigo-400">Psixologiya</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>O'zingizni seving</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Ijobiy fikrlashni o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Stress bilan kurashish usullarini</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Meditatsiya qiling</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-code text-4xl text-cyan-400 mb-3"></i>
                <h3 class="text-xl font-bold text-cyan-400">Texnologiya</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Yangiliklarni kuzatib boring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Dasturlash o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Digital mahoratni rivojlantiring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Sitronaviy xavfsizlikni</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-palette text-4xl text-pink-400 mb-3"></i>
                <h3 class="text-xl font-bold text-pink-400">Ijodkorlik</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Ijodiy qobiliyatlarni rivojlantiring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Rasm chizing yoki yozing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Musiqa tinglang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Badiiy asarlar o'qing</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-globe text-4xl text-teal-400 mb-3"></i>
                <h3 class="text-xl font-bold text-teal-400">Til O'rganish</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Kunlik 30 daqiqa o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Filmlar va seriallar tomosha qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Nutqni mashq qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Madaniyat haqida o'rganing</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-leaf text-4xl text-green-500 mb-3"></i>
                <h3 class="text-xl font-bold text-green-500">Ekologiya</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Atrofmizni himoya qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Qayta ishlatishni o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Energiya tejang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Tabiiy mahsulotlarni tanlang</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-book text-4xl text-orange-400 mb-3"></i>
                <h3 class="text-xl font-bold text-orange-400">Kitob O'qish</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Kunlik 20 sahifa o'qing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Turli janrlarni sinab ko'ring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Notebook yarating</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Kitob klublariga qo'shiling</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-utensils text-4xl text-red-500 mb-3"></i>
                <h3 class="text-xl font-bold text-red-500">Oshxona</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Yangi taomlar tayyorlang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Mahalliy ingredientlardan foydalaning</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Ovqat tayyorlash san'atini</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Oilaviy retseptlarni saqlang</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-hiking text-4xl text-emerald-400 mb-3"></i>
                <h3 class="text-xl font-bold text-emerald-400">Sayohat</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Yangi joylarni kashf qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Mahalliy madaniyatni o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Foto va video qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Xotiralarni yozing</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-seedling text-4xl text-lime-400 mb-3"></i>
                <h3 class="text-xl font-bold text-lime-400">Bog'dorchilik</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>O'simliklar ekib o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Tabiat bilan aloqada bo'ling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>O'z sabzavotingizni yetishtiring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Ekologik hayot tarzini</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-dumbbell text-4xl text-red-600 mb-3"></i>
                <h3 class="text-xl font-bold text-red-600">Sport</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Kunlik 30 daqiqa mashq qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Turli sport turlarini sinab ko'ring</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Guruh mashqlariga qo'shiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Sport o'yinlarini tomosha qiling</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-music text-4xl text-violet-400 mb-3"></i>
                <h3 class="text-xl font-bold text-violet-400">Musiqa</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Musiqa asboblarini o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Turli janrlarni tinglang</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Qo'shiq aytishni mashq qiling</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Konsertlarga boring</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-puzzle-piece text-4xl text-amber-400 mb-3"></i>
                <h3 class="text-xl font-bold text-amber-400">O'yinlar</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Zamonaviy va an'anaviy o'yinlar</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Strategiya o'yinlarini o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Oilaviy o'yin kechalarini</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Intellektual mashqlarni</li>
              </ul>
            </div>

            <div class="glass rounded-2xl p-6 hover:scale-105 transition-transform">
              <div class="text-center mb-4">
                <i class="fas fa-handshake text-4xl text-rose-400 mb-3"></i>
                <h3 class="text-xl font-bold text-rose-400">Hamkorlik</h3>
              </div>
              <ul class="space-y-2 text-sm text-gray-300">
                <li><i class="fas fa-check text-green-400 mr-2"></i>Jamoa ishini o'rganing</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Muloqot qobiliyatlarini</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Liderlik xususiyatlarini</li>
                <li><i class="fas fa-check text-green-400 mr-2"></i>Konfliktlarni hal qilishni</li>
              </ul>
            </div>
          </div>
          
          <div class="text-center mt-8">
            <div class="glass rounded-2xl p-6 inline-block">
              <h3 class="text-xl font-bold mb-4 text-primary">Shaxsiy AI Maslahatchi Kerakmi?</h3>
              <p class="text-gray-300 mb-4">
                PRO yoki ADVANCED rejimni tanlang va shaxsiy maslahatlar oling!
              </p>
              <div class="flex flex-col sm:flex-row gap-3 justify-center">
                <button @click="selectPlan('pro')" class="bg-gradient-to-r from-yellow-500 to-yellow-600 px-6 py-3 rounded-lg font-semibold hover:scale-105 transition-transform">
                  <i class="fas fa-star mr-2"></i>PRO Rejim
                </button>
                <button @click="selectPlan('advanced')" class="bg-gradient-to-r from-purple-500 to-purple-600 px-6 py-3 rounded-lg font-semibold hover:scale-105 transition-transform">
                  <i class="fas fa-crown mr-2"></i>ADVANCED Rejim
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Chat Interface -->
        <div class="max-w-4xl mx-auto">
          <div ref="chatContainer" class="glass rounded-2xl overflow-hidden">
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
                <input ref="chatInput" v-model="currentMessage" @keyup.enter="sendMessage(currentMessage)" 
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
      // Bepul versiyada AI ishlamaydi
      if (this.currentPlan === 'free') return false;
      
      if (this.currentPlan === 'advanced' && this.isAuthenticated) return true;
      if (this.currentPlan === 'pro' && this.isAuthenticated) return this.dailyUsage < this.usageLimit;
      return false;
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
      console.log('startChat called!');
      console.log('currentPlan:', this.currentPlan);
      console.log('isAuthenticated:', this.isAuthenticated);
      
      if (this.currentPlan === 'free') {
        console.log('FREE plan - AI not available');
        // Bepul versiyada AI ishlamaydi, faqat reklama xabari
        this.messages.push({ 
          text: "😔 Bepul versiyada AI maslahatchi mavjud emas. Professional maslahatlar uchun PRO yoki ADVANCED rejimni tanlang!", 
          sender: 'bot', 
          timestamp: new Date() 
        });
        console.log('FREE plan message added - AI disabled');
        
        // Chat qismiga scroll qilish
        this.$nextTick(() => {
          this.scrollToChat();
        });
        
      } else if (this.currentPlan === 'pro' || this.currentPlan === 'advanced') {
        if (this.isAuthenticated) {
          console.log('Starting authenticated chat...');
          // Agar allaqachon authenticated bo'lsa, to'g'ridan-to'g'ri chat boshlash
          this.messages.push({ 
            text: "Salom! Maslahatchi AI ga xush kelibsiz. Sizga qanday yordam bera olaman?", 
            sender: 'bot', 
            timestamp: new Date() 
          });
          
          // Chat qismiga scroll qilish
          this.$nextTick(() => {
            this.scrollToChat();
          });
          
        } else {
          console.log('Opening token modal...');
          // Agar authenticated bo'lmasa, token modal ochish
          this.showTokenModal = true;
        }
      }
    },
    async sendMessage(text, sender = 'user') {
      if (sender === 'user') {
        // Bepul versiyada AI ishlamaydi
        if (this.currentPlan === 'free') {
          this.messages.push({ 
            text: "😔 Bepul versiyada AI maslahatchi mavjud emas. Professional maslahatlar uchun PRO yoki ADVANCED rejimni tanlang!", 
            sender: 'bot', 
            timestamp: new Date() 
          });
          return;
        }
        
        if (!this.canSendMessage) {
          alert(`Sizning kunlik limit (${
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
          // Faqat PRO va ADVANCED rejimlarda Gemini AI ishlatamiz
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
      console.log('selectPlan called with plan:', plan);
      console.log('Current state - currentPlan:', this.currentPlan, 'isAuthenticated:', this.isAuthenticated);
      
      if (plan === 'free') {
        // FREE rejimni to'g'ridan-to'g'ri tanlash mumkin
        this.currentPlan = 'free';
        this.isAuthenticated = false;
        console.log('FREE rejim tanlandi - currentPlan set to free');
      } else if (plan === 'pro' || plan === 'advanced') {
        if (this.isAuthenticated && this.currentPlan === plan) {
          // Agar allaqachon authenticated bo'lsa, hech narsa qilmaymiz
          console.log(`${plan.toUpperCase()} rejim allaqachon faol`);
        } else {
          // Tanlangan planni saqlash va token modal ochish
          this.selectedPlan = plan;
          this.showTokenModal = true;
          console.log(`${plan.toUpperCase()} rejim uchun token modal ochildi - selectedPlan:`, this.selectedPlan);
        }
      }
    },
    scrollToChat() {
      console.log('Scrolling to chat...');
      if (this.$refs.chatContainer) {
        this.$refs.chatContainer.scrollIntoView({ 
          behavior: 'smooth',
          block: 'start'
        });
        console.log('Scrolled to chat container');
        
        // Chat input ga focus qilish
        setTimeout(() => {
          if (this.$refs.chatInput) {
            this.$refs.chatInput.focus();
            console.log('Chat input focused');
          }
        }, 500); // Scroll tugagandan keyin focus qilish
        
      } else {
        console.log('Chat container ref not found');
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