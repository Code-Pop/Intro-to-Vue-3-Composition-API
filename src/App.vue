<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = true
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 2234, color: 'green'},
  { id: 2234, color: 'blue'}
])
const sizes = ref (['39', '40', '41', '42', '43', '44', '45'])
</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div v-for="varian in variants" :key="varian.id">{{ varian.color }}</div>
        <ul>
          <li v-for="size in sizes">{{ size }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>