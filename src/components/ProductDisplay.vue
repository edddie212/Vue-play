<template>

      <div class="product-image">
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p>{{ description }}</p>
        <p v-if="inventory > 10">In Stock.</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out</p>
        <p v-else>Out of Stock!</p>
        <p> Shipping: {{shipping}}</p>
        <ul>
          <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
        </ul>

        <p v-if="onSale">On Sale</p>
        <div>
         <span v-for="(variant, index) in variants"
               :class="variant.color"
               :key="variant.id"
               @mouseover="updateVariant(index)">asd
        </span>

        </div>
        <button class="button"
                :class="{disabledButton: !inStock}"
                :disabled="!inStock"
                @click="addToCart">Add to cart</button>

      </div>
  <ReviewForm @review-submitted="addReview" />

  <div v-if="reviews.length" class="container">
    <ReviewList :reviews="reviews" />
  </div>
</template>

<script>
import ReviewForm from "./ReviewForm";
import ReviewList from "./ReviewList";

export default {
  name: "ProductDisplay",
  components: {ReviewForm, ReviewList},
  props: {
    premium: {
      type: Boolean,
      required: true
    },
  },
  data() {
    return {
      product: 'Socks',
      brand: 'Chill Zaur',
      description: 'This is socks.',
      selectedVariant: 0,
      inventory: 12,
      onSale: true,
      details: ['50% cotton', '30%woll', '20% polyester'],
      variants: [
        {id: 2234, color: 'green', image: './assets/images/socks_green.jpg', quantity: 50},
        {id: 2235, color: 'blue', image: './assets/images/socks_blue.jpg', quantity: 0},
      ],
      reviews: []
    }
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].id)
      this.inventory--
    },
    updateVariant(index) {
      this.selectedVariant = index;
    },
    addReview(review){
     this.reviews.push(review)
    }
  },
  computed: {
    title() {
      return this.brand + ' ' +  this.product
    },
    image(){
      return this.variants[this.selectedVariant].image
    },
    inStock(){
      return  this.variants[this.selectedVariant].quantity
    },
    shipping(){
      if(this.premium){
        return 'Free'
      }
      return 2.99
    }
  }
}
</script>

<style scoped>

</style>