<template>
    <div class="col-md-4 mb-4">
      <div class="card">
        <img :src="product.image" class="card-img-top" alt="Product Image">
        <div class="card-body">
          <h5 class="card-title">{{ product.name }}</h5>
          <p class="card-text">Price: ${{ product.price }}</p>
          <button @click="$emit('add-to-cart', product)" class="btn btn-primary">Add to Cart</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProductItem',
    props: {
      product: Object
    }
  };
  </script>
  
  <style scoped>
  .card {
    width: 100%;
  }
  .card-img-top {
    width: 100%;
    height: auto;
  }
  </style>
  