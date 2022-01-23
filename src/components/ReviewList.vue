<template>
  <div class="review-container">
    <h3>Reviews</h3>
    <ul>
        <div :style="{
          padding: '1rem',
          border: '2px solid #000',
          borderRadius: '1rem',
          marginRight: '2rem'
        }">
          <li
              class="card-title"
              v-for="(review, index) in  reviews"
              :key="index">{{review.name}}
            gave this {{review.rating}} stars
            <br/>
            <p class="card-body">"{{review.review}}"</p>
          </li>
        </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ReviewList",
  props: {
    reviews: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>

</style>