<template>
  <footer class="bg-black/20 border-t border-white/10 dark:bg-black/20 dark:border-white/10 light:bg-white/90 light:border-gray-200">
    <div class="max-w-7xl mx-auto px-4 py-12">
      <div class="grid md:grid-cols-4 gap-8">
        <div>
          <div class="flex items-center space-x-2 mb-4">
            <i class="fas fa-robot text-2xl text-primary"></i>
            <span class="text-xl font-bold gradient-text">Maslahatchi AI</span>
          </div>
          <p class="text-gray-300">Professional AI maslahatchi xizmatlari barcha sohalarda</p>
        </div>
        <div>
          <h3 class="font-semibold mb-4">Xizmatlar</h3>
          <ul class="space-y-2 text-gray-300">
            <li>Bepul maslahat</li>
            <li>Pro rejim</li>
            <li>Advanced rejim</li>
            <li>Maxsus yechimlar</li>
          </ul>
        </div>
        <div>
          <h3 class="font-semibold mb-4">Kompaniya</h3>
          <ul class="space-y-2 text-gray-300">
            <li><router-link to="/about" class="hover:text-primary transition-colors">Biz haqimizda</router-link></li>
            <li><router-link to="/help" class="hover:text-primary transition-colors">Yordam</router-link></li>
            <li><router-link to="/pricing" class="hover:text-primary transition-colors">Narxlar</router-link></li>
            <li><router-link to="/features" class="hover:text-primary transition-colors">Xususiyatlar</router-link></li>
          </ul>
        </div>
        <div>
          <h3 class="font-semibold mb-4">Aloqa</h3>
          <div class="space-y-2 text-gray-300">
            <p><i class="fab fa-telegram mr-2"></i>@Dier_Ai</p>
            <p><i class="fas fa-envelope mr-2"></i>info@maslahatchi.ai</p>
          </div>
        </div>
      </div>
      <div class="border-t border-white/10 mt-8 pt-8 text-center text-gray-300">
        <p>&copy; 2025 Maslahatchi AI. Barcha huquqlar himoyalangan.</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style scoped>
.text-primary {
  color: #6366f1;
}
</style>
