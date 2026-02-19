<template>
  <div id="app" class="container">
    <h1>HelloPrint Portfolio Demo: Product Selector</h1>
    
    <div class="product-grid">
      <div v-for="item in products" :key="item.id" class="card">
        <h3>{{ item.name }}</h3>
        <p>Starting at: ₱{{ item.price }}</p>
        <button @click="addToCart(item)">Add to Order</button>
      </div>
    </div>

    <div class="cart">
      <h2>Your Selection ({{ cartCount }} items)</h2>
      <ul>
        <li v-for="(item, index) in cart" :key="index">
          {{ item.name }} - ₱{{ item.price }}
        </li>
      </ul>
      <p><strong>Total: ₱{{ totalCost }}</strong></p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const products = ref([
  { id: 1, name: 'Premium Business Cards', price: 500 },
  { id: 2, name: 'Eco-Friendly Flyers', price: 1200 },
  { id: 3, name: 'Company Hoodies', price: 2500 }
]);

const cart = ref([]);

const addToCart = (product) => {
  cart.value.push(product);
};

const cartCount = computed(() => cart.value.length);
const totalCost = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0));
</script>

<style>
.container { font-family: sans-serif; max-width: 800px; margin: auto; }
.product-grid { display: flex; gap: 20px; }
.card { border: 1px solid #ddd; padding: 15px; border-radius: 8px; flex: 1; }
.cart { margin-top: 30px; padding: 20px; background: #f9f9f9; border-radius: 8px; }
button { background: #ff5000; color: white; border: none; padding: 10px; cursor: pointer; }
</style>
