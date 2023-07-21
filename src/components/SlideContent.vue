<script setup>
import SlideHeader from './SlideHeader.vue'
defineProps(['topic', 'title', 'type'])
</script>

<template>
  <div>
    <SlideHeader>{{ topic }}</SlideHeader>
    <div class="slide">
      <h2 class="slide-header">{{ title }}</h2>
      <div class="content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.slide {
  display: flex;
  flex-direction: column;
  padding: 2em;
  gap: 1em;

  h2 {
    font-weight: bold;
    font-size: 2em;
    color: red;
  }
  .content {
    display: flex;
    flex-direction: row;
    gap: 1em;
    font-size: 1.2em;
  }
}
</style>
