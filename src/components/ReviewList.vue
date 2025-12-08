<script setup>

const props = defineProps({
  reviewList: {
    type: Array,
    required: true
  }
})

</script>

<template>
  <div class="review-container">
    <h3>Commentaires:</h3>

    <ul v-if="props.reviewList.length">
      <li v-for="(r, index) in props.reviewList" :key="index">
        <p><strong>{{ index + 1 }}</strong></p>
        <p><strong>name</strong> {{ r.name }}</p>
        <p><strong>review</strong> {{ r.review }}</p>
        <p><strong>rating</strong> {{ r.rating }}</p>
      </li>
    </ul>
    <p v-else>Aucun commentaire.</p>
  </div>
</template>

<style scoped>

</style>