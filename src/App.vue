<script setup>
import { ref } from 'vue'
import ProductDisplay from './components/ProductDisplay.vue'

const cart = ref([])
const premium = ref(1)
const updateCart = (id) => {
  cart.value.push(id)
}
const removeFromCart = (id) => {
  const index = cart.value.indexOf(id)
  if (index !== -1) {
    cart.value.splice(index, 1)
  }
}
</script>
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart.length }})</div>
  <ProductDisplay :premium="premium" @add-to-cart="updateCart" @remove-from-cart="removeFromCart" />
</template>