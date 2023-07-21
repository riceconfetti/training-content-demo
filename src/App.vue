<script setup>
import ContentContainer from './components/ContentContainer.vue'

const courseData = {
  "courseCode": "L210E",
  "courseTitle": "Financials Process Overview",
  "topic": "Finance"
}
</script>

<template>
    <ContentContainer v-bind="courseData"/>
</template>

<style scoped lang="scss">

</style>
