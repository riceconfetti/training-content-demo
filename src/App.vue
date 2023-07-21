<script setup>
import ContentContainer from './components/ContentContainer.vue'

const courseData = {
  "courseCode": "E300",
  "courseTitle": "Test Course Title",
  "topic": "Introduction To Learning"
}
</script>

<template>
    <ContentContainer v-bind="courseData"/>
</template>

<style scoped lang="scss">

</style>
