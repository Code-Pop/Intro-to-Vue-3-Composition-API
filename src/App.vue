<script setup>
import { ref } from 'vue'
import productDisplay from '@/components/productDisplay.vue';

const cart = ref(0)
const premium = ref(true)

</script>

<template>
  <div class="nav-bar"></div>
  <button class="cart">Cart({{ cart }})</button>
  <productDisplay :premium="premium" ></productDisplay>
</template>


