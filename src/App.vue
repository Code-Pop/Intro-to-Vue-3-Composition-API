<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const iventory = ref(15)
const onSale = ref(true)

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
        <p v-if="iventory > 10">In Stock</p>
        <p v-else-if="iventory <= 10 && iventory > 0">Almost sold out!</p>
        <p v-else>Out of stock</p>
        <p v-show="onSale">On Sale</p>
      </div>
    </div>
  </div>
</template>