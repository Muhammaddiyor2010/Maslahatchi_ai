<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-7xl mx-auto">
      <!-- Hero Section -->
      <div class="text-center mb-16">
        <h1 class="text-4xl md:text-6xl font-bold mb-6 gradient-text">Yordam Markazi</h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          Maslahatchi AI xizmatidan foydalanish bo'yicha barcha savollaringizga javob toping
        </p>
      </div>

      <!-- Search Section -->
      <div class="mb-16">
        <div class="glass rounded-2xl p-8 max-w-2xl mx-auto">
          <h2 class="text-2xl font-bold text-center mb-6">Qidiruv</h2>
          <div class="relative">
            <input 
              v-model="searchQuery"
              type="text" 
              placeholder="Savolingizni yozing..."
              class="w-full bg-gray-800 border border-gray-600 rounded-lg px-4 py-3 pr-12 text-white focus:border-primary focus:outline-none"
            >
            <i class="fas fa-search absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400"></i>
          </div>
        </div>
      </div>

      <!-- Quick Help Categories -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Tezkor Yordam</h2>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div v-for="category in quickHelpCategories" :key="category.title"
               class="glass rounded-2xl p-6 text-center hover:scale-105 transition-transform cursor-pointer"
               @click="scrollToSection(category.id)">
            <i :class="category.icon + ' text-4xl text-primary mb-4'"></i>
            <h3 class="text-lg font-bold mb-2">{{ category.title }}</h3>
            <p class="text-gray-300 text-sm">{{ category.description }}</p>
          </div>
        </div>
      </div>

      <!-- FAQ Section -->
      <div class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Tez-tez So'raladigan Savollar</h2>
        <div class="max-w-4xl mx-auto space-y-4">
          <div v-for="(faq, index) in filteredFAQs" :key="index" 
               class="glass rounded-lg overflow-hidden">
            <button 
              @click="toggleFAQ(index)"
              class="w-full text-left p-6 flex justify-between items-center hover:bg-white/5 transition-colors">
              <h3 class="font-semibold text-lg">{{ faq.question }}</h3>
              <i :class="faq.isOpen ? 'fas fa-chevron-up' : 'fas fa-chevron-down'" 
                 class="text-primary transition-transform"></i>
            </button>
            <div v-if="faq.isOpen" class="px-6 pb-6">
              <div class="text-gray-300" v-html="faq.answer"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Getting Started Guide -->
      <div id="getting-started" class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Boshlash Qo'llanmasi</h2>
        <div class="grid md:grid-cols-2 gap-8">
          <div v-for="(step, index) in gettingStartedSteps" :key="index"
               class="glass rounded-2xl p-6">
            <div class="flex items-start space-x-4">
              <div class="bg-primary text-white rounded-full w-8 h-8 flex items-center justify-center font-bold flex-shrink-0">
                {{ index + 1 }}
              </div>
              <div>
                <h3 class="text-xl font-bold mb-3">{{ step.title }}</h3>
                <p class="text-gray-300">{{ step.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Site Usage Guide -->
      <div id="site-usage" class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Saytni Ishlatish Haqida Yo'riqnoma</h2>
        
        <!-- Navigation Guide -->
        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-6 text-center">Sayt Navigatsiyasi</h3>
          <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
            <div v-for="nav in navigationGuide" :key="nav.title"
                 class="glass rounded-lg p-6 text-center">
              <i :class="nav.icon + ' text-3xl text-primary mb-4'"></i>
              <h4 class="font-bold mb-2">{{ nav.title }}</h4>
              <p class="text-gray-300 text-sm mb-3">{{ nav.description }}</p>
              <router-link :to="nav.link" 
                           class="text-primary hover:underline text-sm">
                O'tish →
              </router-link>
            </div>
          </div>
        </div>

        <!-- Main Features Usage -->
        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-6 text-center">Asosiy Funksiyalar</h3>
          <div class="space-y-8">
            <div v-for="feature in mainFeaturesUsage" :key="feature.title"
                 class="glass rounded-2xl p-8">
              <div class="flex items-center mb-6">
                <i :class="feature.icon + ' text-4xl text-primary mr-4'"></i>
                <div>
                  <h4 class="text-2xl font-bold">{{ feature.title }}</h4>
                  <p class="text-gray-300">{{ feature.subtitle }}</p>
                </div>
              </div>
              
              <div class="grid md:grid-cols-2 gap-6">
                <div>
                  <h5 class="font-semibold mb-3 text-primary">Qanday ishlatish:</h5>
                  <ol class="list-decimal list-inside space-y-2 text-gray-300">
                    <li v-for="step in feature.usageSteps" :key="step">{{ step }}</li>
                  </ol>
                </div>
                <div>
                  <h5 class="font-semibold mb-3 text-primary">Maslahatlar:</h5>
                  <ul class="list-disc list-inside space-y-2 text-gray-300">
                    <li v-for="tip in feature.tips" :key="tip">{{ tip }}</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Account Management -->
        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-6 text-center">Hisob Boshqaruvi</h3>
          <div class="grid md:grid-cols-2 gap-8">
            <div v-for="account in accountManagement" :key="account.title"
                 class="glass rounded-lg p-6">
              <div class="flex items-center mb-4">
                <i :class="account.icon + ' text-2xl text-primary mr-3'"></i>
                <h4 class="text-xl font-bold">{{ account.title }}</h4>
              </div>
              <p class="text-gray-300 mb-4">{{ account.description }}</p>
              <div class="bg-gray-800 rounded-lg p-4">
                <h5 class="font-semibold mb-2">Qadamlar:</h5>
                <ol class="list-decimal list-inside space-y-1 text-gray-300 text-sm">
                  <li v-for="step in account.steps" :key="step">{{ step }}</li>
                </ol>
              </div>
            </div>
          </div>
        </div>

        <!-- Mobile Usage -->
        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-6 text-center">Mobil Qurilmalarda Ishlatish</h3>
          <div class="glass rounded-2xl p-8">
            <div class="grid md:grid-cols-2 gap-8">
              <div>
                <h4 class="text-xl font-bold mb-4">Smartfon va Planshet</h4>
                <ul class="space-y-3 text-gray-300">
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-400 mr-3 mt-1"></i>
                    <span>Responsive dizayn - barcha ekran o'lchamlarida yaxshi ko'rinadi</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-400 mr-3 mt-1"></i>
                    <span>Touch-friendly interfeys - barmoq bilan oson ishlatish</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-400 mr-3 mt-1"></i>
                    <span>Tez yuklash - optimallashtirilgan mobil versiya</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-400 mr-3 mt-1"></i>
                    <span>Offline rejim - ba'zi funksiyalar internet bo'lmasa ham ishlaydi</span>
                  </li>
                </ul>
              </div>
              <div>
                <h4 class="text-xl font-bold mb-4">Mobil Maslahatlar</h4>
                <ul class="space-y-3 text-gray-300">
                  <li class="flex items-start">
                    <i class="fas fa-lightbulb text-yellow-400 mr-3 mt-1"></i>
                    <span>Brauzer cache'ini tozalang - tezroq ishlash uchun</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-lightbulb text-yellow-400 mr-3 mt-1"></i>
                    <span>Wi-Fi yoki 4G/5G ulanishini tekshiring</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-lightbulb text-yellow-400 mr-3 mt-1"></i>
                    <span>Brauzer yangilanishini o'tkazib yubormang</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-lightbulb text-yellow-400 mr-3 mt-1"></i>
                    <span>Bookmark qiling - tezroq kirish uchun</span>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>

        <!-- Keyboard Shortcuts -->
        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-6 text-center">Klaviatura Qisqartmalari</h3>
          <div class="glass rounded-2xl p-8">
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
              <div v-for="shortcut in keyboardShortcuts" :key="shortcut.action"
                   class="bg-gray-800 rounded-lg p-4">
                <div class="flex items-center justify-between">
                  <span class="text-gray-300">{{ shortcut.action }}</span>
                  <kbd class="bg-gray-700 text-white px-2 py-1 rounded text-sm font-mono">
                    {{ shortcut.key }}
                  </kbd>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Features Guide -->
      <div id="features" class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Xususiyatlar Qo'llanmasi</h2>
        <div class="space-y-8">
          <div v-for="feature in featuresGuide" :key="feature.title"
               class="glass rounded-2xl p-8">
            <div class="flex items-center mb-4">
              <i :class="feature.icon + ' text-3xl text-primary mr-4'"></i>
              <h3 class="text-2xl font-bold">{{ feature.title }}</h3>
            </div>
            <p class="text-gray-300 mb-4">{{ feature.description }}</p>
            <div class="bg-gray-800 rounded-lg p-4">
              <h4 class="font-semibold mb-2">Qanday ishlatish:</h4>
              <ol class="list-decimal list-inside space-y-2 text-gray-300">
                <li v-for="step in feature.steps" :key="step">{{ step }}</li>
              </ol>
            </div>
          </div>
        </div>
      </div>

      <!-- Troubleshooting -->
      <div id="troubleshooting" class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Muammolarni Hal Qilish</h2>
        <div class="space-y-6">
          <div v-for="issue in troubleshooting" :key="issue.problem"
               class="glass rounded-lg p-6">
            <h3 class="text-xl font-bold mb-3 text-red-400">{{ issue.problem }}</h3>
            <div class="text-gray-300">
              <p class="mb-3"><strong>Sabab:</strong> {{ issue.cause }}</p>
              <div>
                <strong>Yechim:</strong>
                <ul class="list-disc list-inside mt-2 space-y-1">
                  <li v-for="solution in issue.solutions" :key="solution">{{ solution }}</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Contact Support -->
      <div id="contact-support" class="mb-16">
        <h2 class="text-3xl font-bold text-center mb-12">Qo'llab-quvvatlash</h2>
        <div class="glass rounded-2xl p-8 text-center">
          <i class="fas fa-headset text-6xl text-primary mb-6"></i>
          <h3 class="text-2xl font-bold mb-4">Yordam kerakmi?</h3>
          <p class="text-gray-300 mb-8 max-w-2xl mx-auto">
            Agar sizning savolingiz bu yerda javob topilmagan bo'lsa, bizning qo'llab-quvvatlash jamoamizga murojaat qiling.
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <a href="https://t.me/Dier_Ai" target="_blank"
               class="inline-flex items-center bg-blue-600 hover:bg-blue-700 px-6 py-3 rounded-lg font-semibold transition-colors">
              <i class="fab fa-telegram mr-2"></i>
              Telegram orqali yozing
            </a>
            <a href="mailto:Muhammaddiyorjon2010@icloud.com"
               class="inline-flex items-center bg-red-600 hover:bg-red-700 px-6 py-3 rounded-lg font-semibold transition-colors">
              <i class="fas fa-envelope mr-2"></i>
              Email yuboring
            </a>
            <a href="tel:+998931981793"
               class="inline-flex items-center bg-green-600 hover:bg-green-700 px-6 py-3 rounded-lg font-semibold transition-colors">
              <i class="fas fa-phone mr-2"></i>
              Telefon qiling
            </a>
          </div>
        </div>
      </div>

      <!-- Back to Top -->
      <div class="text-center">
        <button @click="scrollToTop"
                class="bg-primary hover:bg-primary/80 px-6 py-3 rounded-lg font-semibold transition-colors">
          <i class="fas fa-arrow-up mr-2"></i>
          Sahifa boshiga qaytish
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Help',
  data() {
    return {
      searchQuery: '',
      quickHelpCategories: [
        {
          title: 'Boshlash',
          description: 'Qanday qilib ishlatishni o\'rganish',
          icon: 'fas fa-play',
          id: 'getting-started'
        },
        {
          title: 'Saytni Ishlatish',
          description: 'Sayt funksiyalarini o\'rganish',
          icon: 'fas fa-desktop',
          id: 'site-usage'
        },
        {
          title: 'Xususiyatlar',
          description: 'Barcha imkoniyatlarni o\'rganish',
          icon: 'fas fa-cogs',
          id: 'features'
        },
        {
          title: 'Muammolar',
          description: 'Muammolarni hal qilish',
          icon: 'fas fa-tools',
          id: 'troubleshooting'
        },
        {
          title: 'Qo\'llab-quvvatlash',
          description: 'Yordam olish',
          icon: 'fas fa-headset',
          id: 'contact-support'
        }
      ],
      faqs: [
        {
          question: 'Maslahatchi AI nima?',
          answer: 'Maslahatchi AI - bu Google Gemini AI texnologiyasidan foydalanib, har qanday sohada professional maslahatlar beruvchi sun\'iy intellekt platformasi. Biz sizga biznes, ta\'lim, texnologiya va boshqa sohalarda yordam beramiz.',
          isOpen: false
        },
        {
          question: 'Qanday qilib ro\'yxatdan o\'tish mumkin?',
          answer: 'Ro\'yxatdan o\'tish juda oson! Bosh sahifadagi "Bepul Boshlash" tugmasini bosing va email manzilingizni kiriting. Keyin sizga tasdiqlash xabari yuboriladi.',
          isOpen: false
        },
        {
          question: 'Xizmat pullikmi?',
          answer: 'Bizning xizmatimizda bepul va pullik rejalar mavjud. Bepul rejada kuniga cheklangan miqdorda savol berishingiz mumkin. Pullik rejalar orqali cheksiz savollar va qo\'shimcha xususiyatlar mavjud.',
          isOpen: false
        },
        {
          question: 'Qanday tillarda maslahat olish mumkin?',
          answer: 'Biz o\'zbek, rus va ingliz tillarida maslahat beramiz. Siz o\'zingizga qulay tilda savol berishingiz mumkin.',
          isOpen: false
        },
        {
          question: 'Javob qachon keladi?',
          answer: 'Bizning AI tizimimiz soniyalar ichida javob beradi. Agar sizning savolingiz murakkab bo\'lsa, javob bir necha daqiqa vaqt olishi mumkin.',
          isOpen: false
        },
        {
          question: 'Ma\'lumotlarim xavfsizmi?',
          answer: 'Ha, barcha ma\'lumotlaringiz xavfsiz va maxfiy. Biz sizning shaxsiy ma\'lumotlaringizni uchinchi shaxslarga bermaymiz va zamonaviy shifrlash texnologiyalaridan foydalanamiz.',
          isOpen: false
        },
        {
          question: 'Qanday qilib hisobni o\'chirish mumkin?',
          answer: 'Hisobingizni o\'chirish uchun qo\'llab-quvvatlash xizmatimizga murojaat qiling. Biz 24 soat ichida sizning so\'rovingizni bajaramiz.',
          isOpen: false
        },
        {
          question: 'Mobil qurilmada ishlatish mumkinmi?',
          answer: 'Ha, bizning platformamiz barcha qurilmalarda - kompyuter, planshet va smartfondan foydalanish uchun optimallashtirilgan.',
          isOpen: false
        }
      ],
      navigationGuide: [
        {
          title: 'Bosh Sahifa',
          description: 'Asosiy sahifa va xizmatlar haqida ma\'lumot',
          icon: 'fas fa-home',
          link: '/'
        },
        {
          title: 'Xususiyatlar',
          description: 'Barcha imkoniyatlar va funksiyalar',
          icon: 'fas fa-star',
          link: '/features'
        },
        {
          title: 'Maslahatlar',
          description: 'AI maslahatchi bilan ishlash',
          icon: 'fas fa-comments',
          link: '/advice'
        },
        {
          title: 'Narxlar',
          description: 'Tarif rejalari va narxlar',
          icon: 'fas fa-tags',
          link: '/pricing'
        },
        {
          title: 'Biz Haqimizda',
          description: 'Kompaniya va aloqa ma\'lumotlari',
          icon: 'fas fa-info-circle',
          link: '/about'
        }
      ],
      mainFeaturesUsage: [
        {
          title: 'AI Maslahatchi',
          subtitle: 'Professional maslahatlar olish',
          icon: 'fas fa-robot',
          usageSteps: [
            'Maslahatlar sahifasiga o\'ting',
            'Savolingizni aniq va batafsil yozing',
            'Sohani belgilang (biznes, ta\'lim, texnologiya)',
            'Javobni kutib turing va o\'qing',
            'Maslahatni saqlang yoki baholang'
          ],
          tips: [
            'Savolni aniq va batafsil yozing',
            'Kontekst va ma\'lumotlarni qo\'shing',
            'Bir vaqtda bir savol bering',
            'Javobni diqqat bilan o\'qing'
          ]
        },
        {
          title: 'Profil Boshqaruvi',
          subtitle: 'Shaxsiy ma\'lumotlarni sozlash',
          icon: 'fas fa-user-cog',
          usageSteps: [
            'Profil sahifasiga o\'ting',
            'Shaxsiy ma\'lumotlarni to\'ldiring',
            'Qiziqish sohalarini belgilang',
            'Parolni o\'zgartiring',
            'Hisob sozlamalarini saqlang'
          ],
          tips: [
            'To\'liq ma\'lumotlarni kiriting',
            'Parolni murakkab qiling',
            'Email manzilini to\'g\'ri yozing',
            'Muntazam ravishda yangilang'
          ]
        },
        {
          title: 'Maslahatlar Tarixi',
          subtitle: 'Avvalgi maslahatlarni ko\'rish',
          icon: 'fas fa-history',
          usageSteps: [
            'Profil sahifasiga o\'ting',
            'Maslahatlar tarixi bo\'limini oching',
            'Kerakli maslahatni toping',
            'Qayta o\'qing yoki nusxa oling',
            'Filtr va qidiruv funksiyalaridan foydalaning'
          ],
          tips: [
            'Muntazam ravishda tekshiring',
            'Muhim maslahatlarni belgilang',
            'Qidiruv funksiyasidan foydalaning',
            'Eski maslahatlarni o\'chiring'
          ]
        }
      ],
      accountManagement: [
        {
          title: 'Hisob Yaratish',
          description: 'Yangi hisob yaratish va ro\'yxatdan o\'tish',
          icon: 'fas fa-user-plus',
          steps: [
            'Bosh sahifadagi "Bepul Boshlash" tugmasini bosing',
            'Email manzilingizni kiriting',
            'Parol yarating (kamida 8 belgi)',
            'Tasdiqlash xabarini kutib turing',
            'Email orqali tasdiqlang'
          ]
        },
        {
          title: 'Parolni Tiklash',
          description: 'Unutilgan parolni tiklash',
          icon: 'fas fa-key',
          steps: [
            'Kirish sahifasida "Parolni unutdingizmi?" ni bosing',
            'Email manzilingizni kiriting',
            'Tiklash xabarini kutib turing',
            'Email orqali yangi parol yarating',
            'Yangi parol bilan kiring'
          ]
        },
        {
          title: 'Hisobni O\'chirish',
          description: 'Hisobni butunlay o\'chirish',
          icon: 'fas fa-user-times',
          steps: [
            'Profil sozlamalariga o\'ting',
            'Hisob o\'chirish bo\'limini toping',
            'Sababni belgilang',
            'Tasdiqlash kodini kiriting',
            'O\'chirishni tasdiqlang'
          ]
        },
        {
          title: 'Ma\'lumotlarni Yangilash',
          description: 'Shaxsiy ma\'lumotlarni o\'zgartirish',
          icon: 'fas fa-edit',
          steps: [
            'Profil sahifasiga o\'ting',
            'O\'zgartirmoqchi bo\'lgan maydonni toping',
            'Yangi ma\'lumotni kiriting',
            'Saqlash tugmasini bosing',
            'Tasdiqlash xabarini kutib turing'
          ]
        }
      ],
      keyboardShortcuts: [
        { action: 'Bosh sahifaga o\'tish', key: 'Ctrl + H' },
        { action: 'Qidiruv qilish', key: 'Ctrl + K' },
        { action: 'Maslahatlar sahifasi', key: 'Ctrl + A' },
        { action: 'Profil sahifasi', key: 'Ctrl + P' },
        { action: 'Yordam sahifasi', key: 'Ctrl + ?' },
        { action: 'Sahifani yangilash', key: 'F5' },
        { action: 'Orqaga qaytish', key: 'Alt + ←' },
        { action: 'Oldinga o\'tish', key: 'Alt + →' }
      ],
      gettingStartedSteps: [
        {
          title: 'Ro\'yxatdan o\'ting',
          description: 'Email manzilingizni kiriting va hisob yarating. Tasdiqlash xabari yuboriladi.'
        },
        {
          title: 'Profilni to\'ldiring',
          description: 'Shaxsiy ma\'lumotlaringizni kiriting va qiziqish sohalaringizni belgilang.'
        },
        {
          title: 'Birinchi savolni bering',
          description: 'Sizga kerakli maslahat so\'rang. AI tizimimiz tez va aniq javob beradi.'
        },
        {
          title: 'Natijalarni baholang',
          description: 'Olingan maslahatlarni baholang va keyingi savollar uchun asos oling.'
        }
      ],
      featuresGuide: [
        {
          title: 'AI Maslahatchi',
          icon: 'fas fa-robot',
          description: 'Har qanday sohada professional maslahatlar oling',
          steps: [
            'Savolingizni aniq va batafsil yozing',
            'Sohani belgilang (biznes, ta\'lim, texnologiya)',
            'AI javobini kutib turing',
            'Maslahatni o\'qing va amalda qo\'llang'
          ]
        },
        {
          title: 'Shaxsiy Profil',
          icon: 'fas fa-user',
          description: 'O\'z profilingizni yarating va maslahatlarni saqlang',
          steps: [
            'Shaxsiy ma\'lumotlaringizni kiriting',
            'Qiziqish sohalaringizni belgilang',
            'Maslahatlarni saqlang va tahlil qiling',
            'Rivojlanish jarayonini kuzating'
          ]
        },
        {
          title: 'Maslahatlar Tarixi',
          icon: 'fas fa-history',
          description: 'Barcha maslahatlaringizni bir joyda ko\'ring',
          steps: [
            'Profil sahifasiga o\'ting',
            'Maslahatlar tarixi bo\'limini oching',
            'Avvalgi maslahatlarni ko\'ring',
            'Kerakli maslahatlarni qayta o\'qing'
          ]
        }
      ],
      troubleshooting: [
        {
          problem: 'Savol yuborishda xatolik',
          cause: 'Internet aloqasi yoki server muammosi',
          solutions: [
            'Internet aloqangizni tekshiring',
            'Sahifani yangilang (F5)',
            'Brauzer cache\'ini tozalang',
            'Boshqa brauzer bilan sinab ko\'ring'
          ]
        },
        {
          problem: 'Javob kelmayapti',
          cause: 'Server yuklanishi yoki murakkab savol',
          solutions: [
            'Bir necha daqiqa kuting',
            'Savolni qisqaroq qiling',
            'Sahifani yangilang',
            'Qo\'llab-quvvatlash xizmatiga murojaat qiling'
          ]
        },
        {
          problem: 'Hisobga kira olmayman',
          cause: 'Noto\'g\'ri parol yoki email',
          solutions: [
            'Email va parolni qayta tekshiring',
            'Parolni tiklash funksiyasidan foydalaning',
            'Email spam papkasini tekshiring',
            'Qo\'llab-quvvatlash xizmatiga yozing'
          ]
        }
      ]
    }
  },
  computed: {
    filteredFAQs() {
      if (!this.searchQuery) return this.faqs;
      
      return this.faqs.filter(faq => 
        faq.question.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        faq.answer.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  },
  methods: {
    toggleFAQ(index) {
      this.faqs[index].isOpen = !this.faqs[index].isOpen;
    },
    scrollToSection(sectionId) {
      const element = document.getElementById(sectionId);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
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
