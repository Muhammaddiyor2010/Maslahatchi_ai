<template>
  <div class="about">
    <div class="container">
      <h1>About Us</h1>
      <div class="card">
        <h2>Our Story</h2>
        <p>This is a Vue.js application demonstrating routing functionality. We're using Vue Router to navigate between different pages.</p>
        
        <h3>Features:</h3>
        <ul>
          <li>Vue 3 Composition API</li>
          <li>Vue Router 4</li>
          <li>Tailwind CSS</li>
          <li>Vite Build Tool</li>
        </ul>
      </div>
      
      <div class="card">
        <h2>Contact Information</h2>
        <p>Email: info@example.com</p>
        <p>Phone: +1 (555) 123-4567</p>
        <p>Address: 123 Main St, City, State 12345</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'About'
}
</script>

<style scoped>
.about {
  padding: 2rem 0;
}

ul {
  list-style-type: disc;
  margin-left: 2rem;
  margin-top: 1rem;
}

li {
  margin-bottom: 0.5rem;
}
</style>
