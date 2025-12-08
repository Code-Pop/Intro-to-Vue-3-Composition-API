<script setup>
import { ref } from 'vue'
import socksGreenImage from '../assets/images/socks_green.jpeg'
import socksBlueImage from '../assets/images/socks_blue.jpeg'
import ProductDetails from "@/components/ProductDetails.vue";
import ReviewForm from "@/components/ReviewForm.vue";
import ReviewList from "@/components/ReviewList.vue";

const product = ref('Socks')
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 0, color: 'green', image: socksGreenImage, quantity: 10, onSale: true},
  { id: 1, color: 'blue', image: socksBlueImage, quantity: 20, onSale: false},
])
const brand = ref('CPNV')
const selectedVariant = ref(0)
const shipping = ref(null)
const reviewList = ref([])

const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['add-to-cart'],[remove-from-cart])

function sale(){
  if (variants.value[selectedVariant.value].onSale) {
    return " est en action !"  }
}
function image() {
  return variants.value[selectedVariant.value].image
}
function inStock() {
  return variants.value[selectedVariant.value].quantity > 0
}
function brandedProduct() {
  return brand.value + ' ' + product.value
}
function updateVariant(variantId) {
  selectedVariant.value = variantId
}
function shippingCost(){
  if (props.premium){
    shipping.value = 'Free'
  }
  else{
    shipping.value = 5.99
  }
  return shipping.value
}
function addReview(review){
  reviewList.value.push(review)
}
function addToCart() {
  emit('add-to-cart', variants.value[selectedVariant.value].id)
}
function removeFromCart() {
  emit('remove-from-cart', variants.value[selectedVariant.value].id)
}

</script>
<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-if="inStock()" v-bind:src="image()" alt="Socks"/>
        <img v-else v-bind:src="image()" alt="Socks" class="out-of-stock-img"/>
      </div>
      <div class="product-info">
        <h1>{{ brandedProduct() }}</h1>
        <p>{{ sale() }}</p>
        <p v-if="inStock()">In Stock</p>
        <p v-else>Out of Stock</p>
        <ProductDetails :details="details"></ProductDetails>
        <p>{{shippingCost()}}</p>
        <div class="color-circle"
             v-for="(variant, index) in variants"
             :key="variant.id"
             :style="{ backgroundColor: variant.color }"
             @mouseover="updateVariant(index)"
        >
        </div>
        <button v-if="inStock()" @click="addToCart()" >Ajouter</button>
        <button v-else class="disabledButton">Ajouter</button>
        <button @click="removeFromCart()">Enlever du panier</button>
        <ReviewForm @review-submitted="addReview"></ReviewForm>
        <ReviewList :reviewList="reviewList" />
        <!-- reviewList est une donnée dynamique -->
      </div>
    </div>
  </div>
</template>
