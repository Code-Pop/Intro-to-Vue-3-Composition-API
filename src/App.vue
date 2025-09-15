<script setup>
import { ref } from 'vue'
import ProductDisplay from '@/components/ProductDisplay.vue';

const cart = ref(0)
const premium = ref(true)
const productDetails = ref(['50% cotton', '30% wool', '20% polyester'])

</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <ProductDisplay :premium="premium" :productDetails="productDetails"></ProductDisplay>
</template>