<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['review-submitted'])

const review = reactive({
  name: '',
  content: '', 
  recomend: '',
  rating: null
})

const onSubmit = () => {
  if(review.name === '' || review.content === '' || review.rating === null || review.recomend === '') {
    alert('Review is incomplete. Please fill out every field.')
    return
  }

  const ProductReview = {
    name: review.name,
    content: review.content,
    recomend: review.recomend,
    rating: review.rating
  }
  emit('review-submitted', ProductReview)

  review.name = ''
  review.content = ''
  review.recomend = ''
  review.rating = null
}
</script>

<template>
  <form class="review-form" @submit.prevent ="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="review.name">

    <label for="review">Review:</label>      
    <textarea id="review" v-model="review.content"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="review.rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <label for="recomend">Would you recomend this product?</label>
    <select id="recomend" v-model="review.recomend">
      <option>Yes</option>
      <option>No</option>
    </select>

    <input class="button" type="submit" value="Submit">
  </form>
</template>