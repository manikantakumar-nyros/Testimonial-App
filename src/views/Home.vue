<template>
  <div class="home">
    <TestimonialForm msg="Welcome to Your Vue.js App"/><br/>
    <Carousel msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import TestimonialForm from '@/components/TestimonialForm.vue'
import Carousel from '@/components/Carousel.vue'

export default {
  name: 'home',
  components: {
    TestimonialForm,
    Carousel
  }
}
</script>
