<template>
    <div class="container">
      <h2 class="mt-4 mb-3">Products</h2>
      <div class="row">
        <ProductItem
          v-for="product in products"
          :key="product.id"
          :product="product"
          @add-to-cart="$emit('add-to-cart', product)"
        />
      </div>
    </div>
  </template>
  
  <script>
  import ProductItem from './ProductItem.vue';
  
  export default {
    name: 'ProductList',
    components: {
      ProductItem
    },
    data() {
      return {
        products: [
          { id: 1, name: 'Product 1', price: 100, expirationDate: '2024-06-01', image: '/images/product1.jpg' },
          { id: 2, name: 'Product 2', price: 200, expirationDate: '2024-06-15', image: '/images/product2.jpg' },
          { id: 3, name: 'Product 3', price: 300, expirationDate: '2024-07-01', image: '/images/product3.jpg' }
        ]
      };
    }
  };
  </script>
  