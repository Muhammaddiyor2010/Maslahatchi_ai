<template>
  <div class="not-found">
    <div class="container">
      <div class="error-content">
        <h1>404</h1>
        <h2>Page Not Found</h2>
        <p>The page you're looking for doesn't exist.</p>
        <div class="button-group">
          <router-link to="/" class="button">
            Go Home
          </router-link>
          <button @click="goBack" class="button button-secondary">
            Go Back
          </button>
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
.not-found {
  padding: 4rem 0;
  text-align: center;
}

.error-content h1 {
  font-size: 8rem;
  font-weight: bold;
  color: #ef4444;
  margin: 0;
  line-height: 1;
}

.error-content h2 {
  font-size: 2rem;
  color: #374151;
  margin: 1rem 0;
}

.error-content p {
  font-size: 1.2rem;
  color: #6b7280;
  margin-bottom: 2rem;
}

.button-group {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

@media (max-width: 768px) {
  .error-content h1 {
    font-size: 6rem;
  }
  
  .error-content h2 {
    font-size: 1.5rem;
  }
  
  .button-group {
    flex-direction: column;
    align-items: center;
  }
}
</style>
