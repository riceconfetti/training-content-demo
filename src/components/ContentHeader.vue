<script setup>
import { watch } from 'vue'
import { useSlidesStore } from '@/stores/slides'
import { storeToRefs } from 'pinia'

const slides = useSlidesStore()
const { current } = storeToRefs(slides)
const { total } = slides
let progress = `width: ${(current.value + 1 / total) * 100}%`

watch(current, () => {
  progress = `width: ${((current.value + 1) / total) * 100}%`
  document.getElementById('progress')?.setAttribute('style', `${progress}`)
})

function toggleSidebar() {
  if (document.getElementById('sidebar')?.hasAttribute('style')) {
    document.getElementById('sidebar')?.removeAttribute('style')
  } else {
    document.getElementById('sidebar')?.setAttribute('style', 'display:none')
  }
}

function windowClose() {
  window.close()
}
</script>

<template>
  <nav>
    <div class="heading">
      <h1 id="heading-title">
        Example Course Heading
      </h1>
      <h2 id="heading-subtitle">
        <slot></slot>
      </h2>
    </div>
    <img id="heading-shield" src="/logo.svg" />
    <div class="progress-bar">
      <div id="progress" :style="progress"></div>
    </div>
    <div class="buttons">
      <a id="heading-index" class="btn-med" @click="toggleSidebar">INDEX</a>
      <a id="heading-exit" class="btn-med" @click="windowClose()">X EXIT</a>
    </div>
  </nav>
</template>

<style scoped lang="scss">

nav {
  color: #050505;
  display: grid;
  grid-template-areas: 'a b d d' 'a b f f';
  grid-template-columns: 120px 1fr repeat(2, 0.3fr);
  justify-content: left;
  margin: 1em 4em;

  #heading-shield {
    grid-area: a;
    width: 100px;
    height: auto;
    align-self: center;
    margin: auto;
  }

  .progress-bar {
    grid-area: d;
    align-self: end;
    width: 100%;
    height: 1em;
    background-color: #AAAAAA;
    border-radius: 10px;
    overflow: hidden;
    #progress {
      height: 100%;
      background-color: #005EFF;
    }
  }

  .heading {
    grid-area: b;
    margin: 0% 2%;
    align-self: center;
    #heading-title {
      font-size: 24px;
      line-height: 28px;
    }
    #heading-subtitle {
      font-weight: bold;
      font-family: 'Open Sans';
      color: #005EFF;
      text-transform: capitalize;
      font-size: 16px;
      letter-spacing: 1px;
    }
  }

  .buttons {
    display: flex;
    justify-content: space-between;
    gap: 1em;
    grid-area: f;
    width: 100%;
    padding: 1em 0;
    .btn-med {
      width: 100%;
      &:hover {
        cursor: pointer;
      }
    }
  }
}
</style>
