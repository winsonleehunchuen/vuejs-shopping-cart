<template>
    <div class="container">
      <h2 class="mt-4 mb-3">Shopping Cart</h2>
      <div class="cart-items-container">
        <CartItem
          v-for="item in cartItems"
          :key="item.id"
          :item="item"
          @remove-item="$emit('remove-item', item.id)"
          @update-quantity="updateQuantity"
        />
      </div>
      <div v-if="cartItems.length > 0">
        <p class="mt-4">Total: ${{ total }}</p>
        <button class="btn btn-primary me-3" @click="$emit('clear-cart')">Clear Cart</button>
        <button class="btn btn-danger" @click="$emit('clear-expired')">Clear Expired Items</button>
      </div>
      <div v-else>
        <p class="mt-4">The cart is empty.</p>
      </div>
    </div>
  </template>
  
  <script>
  import CartItem from './CartItem.vue';
  
  export default {
    name: 'ShoppingCart',
    components: {
      CartItem
    },
    props: {
      cartItems: Array
    },
    computed: {
      total() {
        return this.cartItems.reduce((sum, item) => sum + item.price * item.quantity, 0);
      }
    },
    methods: {
      updateQuantity(productId, quantity) {
        this.$emit('update-quantity', productId, quantity);
      }
    }
  };
  </script>
  
  <style>
  .cart-items-container {
    max-height: 300px;
    overflow-y: auto;
  }
  </style>
  