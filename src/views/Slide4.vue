<script setup>
import SlideContent from '../components/SlideContent.vue'
import { useSlidesStore } from '../stores/slides'
import { onBeforeMount } from 'vue';

const slideData = {
    "title": "Proin tristique lacus",
    "type": "content"
}

const slides = useSlidesStore()
const { addSlide } = slides

onBeforeMount(()=>{
  addSlide(slideData, 3)
})
</script>

<template>
  <SlideContent v-bind="slideData">
    <p>
      This training course will introduce you to the process, coordination, and information required
      to understand the Financials process in GFEBS.
    </p>
    <img src="/shield-01.png" />
  </SlideContent>
</template>
