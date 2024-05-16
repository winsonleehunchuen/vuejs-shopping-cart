<template>
  <div id="app" class="container">
    <h1 class="mt-4 mb-3">Shopping Cart</h1>
    <ProductList @add-to-cart="addToCart" />
    <ShoppingCart
      :cartItems="cart"
      @remove-item="removeItem"
      @clear-cart="clearCart"
      @update-quantity="updateQuantity"
      @clear-expired="clearExpired"
    />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  name: 'App',
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      const item = this.cart.find(item => item.id === product.id);
      if (item) {
        item.quantity++;
      } else {
        // Check if the product is expired
        const currentDate = new Date();
        const expirationDate = new Date(product.expirationDate);
        const isExpired = currentDate > expirationDate;
        
        this.cart.push({ ...product, quantity: 1, isExpired });
      }
    },
    removeItem(productId) {
      this.cart = this.cart.filter(item => item.id !== productId);
    },
    clearCart() {
      this.cart = [];
    },
    updateQuantity(productId, quantity) {
      const item = this.cart.find(item => item.id === productId);
      if (item) {
        item.quantity = quantity;
        if (item.quantity <= 0) {
          this.removeItem(productId);
        }
      }
    },
    clearExpired() {
      this.cart = this.cart.filter(item => !item.isExpired);
    }
  }
};
</script>

<style>
#app {
  padding: 20px;
  background-color: #f8f9fa;
}
</style>
