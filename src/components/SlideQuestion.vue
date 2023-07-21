<script setup>
import SlideHeader from './SlideHeader.vue'
import { useSlidesStore } from '@/stores/slides'
import { onUpdated, ref, watch } from 'vue'
import { storeToRefs } from 'pinia'
import { inject } from 'vue'

const slides = useSlidesStore()
const { current, slidesList } = storeToRefs(slides)
const image = ref('qanda.png')
defineProps(['title', 'topic'])

const answer = inject('answer')

onUpdated(() => {
  if (slidesList.value[current.value].viewed === false) {
    slides.disableNext()
  }
})

watch(answer, () => {
  if (answer.value === slidesList.value[current.value].answer) {
    image.value = 'correct.png'
    slidesList.value[current.value].user = answer.value
    slidesList.value[current.value].viewed = true
    if (current.value <= slides.total) {
      slides.enableNext()
    } else {
      slides.disableNext()
    }
  } else {
    image.value = 'incorrect.png'
    slides.disableNext()
    slidesList.value[current.value].user = answer.value
  }
  slides.setCheckpoint()
})
</script>

<template>
  <div>
    <SlideHeader>{{ topic }}</SlideHeader>
    <div class="slide">
      <h2 class="slide-header">{{ title }}</h2>
      <div class="content">
        <div class="left-column">
          <h3><slot name="question"></slot></h3>

          <div class="options">
            <slot name="options"></slot>
          </div>
        </div>

        <div class="right-column">
          <img :src="image" />
        </div>
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
    flex-shrink: 1;
  }
  .content {
    display: flex;
    position:relative;
    flex-direction: row;
    gap: 1em;
    font-size: 1.2em;
    flex-shrink: 1;
    .left-column {
      display: flex;
      width: 100%;
      flex-direction: column;
      gap: 1em;
      .options {
        display: flex;
        gap: 0.5em;
        flex-direction: column;
        list-style-type: none;
        margin-right: 1rem;
        :slotted(.choice) {
          display: flex;
          width: 100%;
          gap: 1em;
          border: 2px solid rgba(11, 69, 194, 0);
          border-radius: 10px;
          transition-duration: 0.2s;

          input[type='radio'] {
            margin-left: 0.5em;
          }

          label {
            width: 100%;
            height: 100%;
            padding: 0.5em;
          }

          &.checked {
            background-color: rgba(11, 69, 194, 0.1);
            border-radius: 10px;
            transition-duration: 0.2s;
            input[type='radio'] + label {
              color: rgba(11, 69, 194, 1);
              padding: 0.5em;
              font-weight: bold;
            }
          }

          &:hover {
            color: rgba(11, 69, 194, 1);
            border: 2px solid rgb(93, 114, 160);
            transition-duration: 0.2s;
            label {
              font-weight: bold;
            }
          }
        }
      }
    }

    .right-column {
      width: 20em;
      display: flex;
      align-items: center;
      height: 100%;
      img {
        width: 20em;
      }
    }
  }
}
</style>
