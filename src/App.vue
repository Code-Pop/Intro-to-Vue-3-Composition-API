<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = ref(false)
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, inStock: false },
  { id: 2235, color: 'blue', image: socksBlueImage, inStock: true },
])

const cart = ref(0)

const addToCart = () => cart.value += 1

const updateVariant  = (variant) => {
  image.value = variant.image
  inStock.value = variant.inStock
}

</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
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
        <div v-for="variant in variants" 
          :key="variant.id"
          @mouseover="updateVariant(variant)"
          class = "color-circle"
          :style="{ backgroundColor: variant.color }"
        >
        </div>
        <button 
          class="button"
          :class="{ disabledButton: !inStock }"
          v-on:click="addToCart"
          :disabled="!inStock"
        >
          Add to cart
        </button>
      </div>
    </div>
  </div>
</template>