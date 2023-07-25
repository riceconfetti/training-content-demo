<script setup>
import SlideContent from '../components/SlideContent.vue'
import { useSlidesStore } from '../stores/slides'
import { onBeforeMount } from 'vue';

const slideData = {
    "title": "Lorem ipsum dolor",
    "type": "content"
}

const slides = useSlidesStore()
const { addSlide } = slides

onBeforeMount(()=>{
  addSlide(slideData, 0)
})
</script>

<template>
  <SlideContent v-bind="slideData">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam faucibus tempus velit. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Donec facilisis odio et sem ultricies ornare. Morbi auctor ipsum eu ligula placerat ornare. Aliquam scelerisque ante nunc, dictum vulputate risus porta nec. 
    </p>
    <img src="/qanda.png" />
  </SlideContent>
</template>

<style scoped>
  img {
    width: 20em;
  }
</style>
