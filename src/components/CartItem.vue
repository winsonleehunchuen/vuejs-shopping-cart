<template>
    <div class="cart-item border rounded p-3 mb-3">
      <div class="row">
        <div class="col-3">
          <img :src="item.image" class="img-fluid" :alt="item.name">
        </div>
        <div class="col-9">
          <h3>{{ item.name }}</h3>
          <p>Price: ${{ item.price }}</p>
          <p>
            Quantity: 
            <input 
              type="number" 
              class="form-control d-inline-block w-auto"
              v-model.number="quantity" 
              @input="updateQuantity"
              min="0"
            />
          </p>
          <button class="btn btn-danger" @click="$emit('remove-item', item.id)">Remove</button>
          <p v-if="item.isExpired" class="expired-message mt-2">This item is expired</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CartItem',
    props: {
      item: Object
    },
    data() {
      return {
        quantity: this.item.quantity
      };
    },
    watch: {
      item: {
        handler(newItem) {
          this.quantity = newItem.quantity;
        },
        deep: true
      }
    },
    methods: {
      updateQuantity() {
        this.$emit('update-quantity', this.item.id, this.quantity);
      }
    }
  };
  </script>
  
  <style>
  .expired-message {
    color: red;
  }
  </style>
  