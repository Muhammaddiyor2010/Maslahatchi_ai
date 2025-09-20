<template>
  <div class="products">
    <div class="container">
      <h1>Our Products</h1>
      
      <div class="product-grid">
        <div class="card product-card" v-for="product in products" :key="product.id">
          <h3>{{ product.name }}</h3>
          <p class="price">${{ product.price }}</p>
          <p>{{ product.description }}</p>
          <button class="button" @click="addToCart(product)">
            Add to Cart
          </button>
        </div>
      </div>
      
      <div class="card" v-if="cart.length > 0">
        <h2>Shopping Cart ({{ cart.length }} items)</h2>
        <div v-for="item in cart" :key="item.id" class="cart-item">
          <span>{{ item.name }} - ${{ item.price }}</span>
          <button class="button button-danger button-small" @click="removeFromCart(item.id)">
            Remove
          </button>
        </div>
        <div class="cart-total">
          <strong>Total: ${{ cartTotal }}</strong>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Products',
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Laptop',
          price: 999,
          description: 'High-performance laptop for work and gaming.'
        },
        {
          id: 2,
          name: 'Smartphone',
          price: 699,
          description: 'Latest smartphone with advanced features.'
        },
        {
          id: 3,
          name: 'Tablet',
          price: 399,
          description: 'Perfect for reading and light productivity.'
        },
        {
          id: 4,
          name: 'Headphones',
          price: 199,
          description: 'Premium wireless headphones with noise cancellation.'
        }
      ],
      cart: []
    }
  },
  computed: {
    cartTotal() {
      return this.cart.reduce((total, item) => total + item.price, 0)
    }
  },
  methods: {
    addToCart(product) {
      this.cart.push(product)
    },
    removeFromCart(productId) {
      const index = this.cart.findIndex(item => item.id === productId)
      if (index > -1) {
        this.cart.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped>
.products {
  padding: 2rem 0;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.product-card {
  text-align: center;
}

.price {
  font-size: 1.5rem;
  font-weight: bold;
  color: #059669;
  margin: 0.5rem 0;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid #e5e7eb;
}

.cart-item:last-child {
  border-bottom: none;
}

.cart-total {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 2px solid #059669;
  font-size: 1.2rem;
}

.button-small {
  padding: 0.25rem 0.5rem;
  font-size: 0.875rem;
}
</style>
