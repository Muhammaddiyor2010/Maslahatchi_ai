<template>
  <div class="pt-24 pb-16 px-4">
    <div class="max-w-4xl mx-auto text-center">
      <div class="glass rounded-2xl p-12">
        <div class="mb-8">
          <i class="fas fa-exclamation-triangle text-8xl text-red-400 mb-6"></i>
          <h1 class="text-8xl font-bold text-red-400 mb-4">404</h1>
          <h2 class="text-3xl font-bold mb-4">Sahifa Topilmadi</h2>
          <p class="text-xl text-gray-300 mb-8">
            Qidirilayotgan sahifa mavjud emas yoki o'chirilgan.
          </p>
        </div>
        
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <router-link to="/" 
                       class="bg-gradient-to-r from-primary to-secondary px-8 py-4 rounded-lg text-lg font-semibold hover:scale-105 transition-transform">
            <i class="fas fa-home mr-2"></i>Bosh Sahifaga Qaytish
          </router-link>
          <button @click="goBack" 
                  class="border-2 border-primary px-8 py-4 rounded-lg text-lg font-semibold hover:bg-primary/10 transition-colors">
            <i class="fas fa-arrow-left mr-2"></i>Orqaga Qaytish
          </button>
        </div>
        
        <div class="mt-8 text-gray-400">
          <p>Yoki quyidagi sahifalardan birini tanlang:</p>
          <div class="flex flex-wrap justify-center gap-4 mt-4">
            <router-link to="/features" class="hover:text-primary transition-colors">Xususiyatlar</router-link>
            <router-link to="/pricing" class="hover:text-primary transition-colors">Narxlar</router-link>
            <router-link to="/contact" class="hover:text-primary transition-colors">Aloqa</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NotFound',
  methods: {
    goBack() {
      this.$router.go(-1)
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
