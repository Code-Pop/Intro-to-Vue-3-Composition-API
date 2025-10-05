<script setup>
import { ref, computed } from 'vue'
import ReviewForm from './ReviewForm.vue'
import ReviewList from '@/components/ReviewList.vue'
import socksGreenImage from '@/assets/images/socks_green.jpeg'
import socksBlueImage from '@/assets/images/socks_blue.jpeg'

const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['add-to-cart'])

const product = ref('Socks')
const brand = ref('Vue Mastery')

const selectedVariant = ref(0)
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity: 50 },
  { id: 2235, color: 'blue', image: socksBlueImage, quantity: 0 },
])

const reviews = ref([])

const title = computed(() => {
  return brand.value + ' ' + product.value
})

const image = computed(() => {
  return variants.value[selectedVariant.value].image
})

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity > 0
})

const shipping = computed(() => {
  if (props.premium) {
    return 'Free'
  }
  else {
    return 2.99
  }
})

const addToCart = () => {
  emit('add-to-cart', variants.value[selectedVariant.value].id)
}

const updateVariant = (index) => {
  selectedVariant.value = index
}

const addReview = (refiew) => {
  reviews.value.push(refiew)
}
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div 
          v-for="(variant, index) in variants" 
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
        >
        </div>
        <button
          class="button" 
          :class="{ disabledButton: !inStock }"
          :disabled="!inStock"
          v-on:click="addToCart"
        >
          Add to cart
        </button>
      </div>
    </div>
    <ReviewList v-if="reviews.length > 0" :reviews="reviews"></ReviewList>
    <ReviewForm @review-submitted="addReview"></ReviewForm>
  </div>
</template>