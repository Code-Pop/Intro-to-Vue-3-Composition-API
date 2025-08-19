<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const url = ref('https://github.com/Paulius-U')

</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
          <a :href="url">GitHub URL</a>
      </div>
    </div>
  </div>
</template>