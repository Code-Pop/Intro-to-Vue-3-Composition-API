<script setup>
import { ref } from 'vue'

const name = ref('')
const review = ref('')
const rating = ref(null)

const emit = defineEmits(['review-submitted'])

function onSubmit() {
  const productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value
  }
  console.log(productReview)
  emit('review-submitted', productReview)

  // remettre les valeurs par défaut après submit review
  name.value = ''
  review.value = ''
  rating.value = null
}
</script>
<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Laissez un commentaire</h3>
    <label for="name">Nom:</label>
    <input id="name" v-model="name"/>

    <label for="review">Commentaire:</label>
    <textarea id="review" v-model="review"></textarea>

    <label for="rating">Note:</label>
    <select id="rating" v-model.number="rating">
      <option v-for="n in 5" :key="n">{{ n }}</option>
    </select>

    <input class="button" type="submit" value="Valider"/>
  </form>
</template>