<script setup>
import { storeToRefs } from 'pinia'
import { useSlidesStore } from '@/stores/slides'
import ContentHeader from '../components/ContentHeader.vue'
import ContentNavigation from './ContentNavigation.vue'
import SideBar from '../components/SideBar.vue'
import views from '../views'

let slidesComp = Object.keys(views).map((key) => {
  return views[key]
})

const slides = useSlidesStore()
const { current } = storeToRefs(slides)

defineProps(['topic', 'courseCode', 'courseTitle'])
</script>

<template>
  <main>
    <ContentHeader>{{ courseCode }} {{ courseTitle }}</ContentHeader>
    <ContentNavigation>
      <div class="content-box">
        <SideBar v-bind="{ topic: topic }"></SideBar>
        <div v-for="(slide, index) in slidesComp" :key="index">
          <component :is="slide" :topic="topic" v-show="index == current"></component>
        </div>
      </div>
    </ContentNavigation>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  height: 100%;
  padding: 1em;
}
.content-box {
  width: 100%;
  height: 100%;
  background-color: white;
}
</style>
