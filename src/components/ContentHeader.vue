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
  <div class="border"></div>
  <nav>
    <div class="heading">
      <h1 id="heading-title">
        Financial<br />
        Management School
      </h1>
      <h2 id="heading-subtitle">
        <slot></slot>
      </h2>
    </div>
    <img id="heading-shield" src="/shield-01.png" />
    <div class="progress-bar">
      <div id="progress" :style="progress"></div>
    </div>
    <div class="buttons">
      <button id="heading-index" class="btn-med" @click="toggleSidebar">INDEX</button>
      <button id="heading-exit" class="btn-med" @click="windowClose()">X EXIT</button>
    </div>
  </nav>
</template>

<style scoped lang="scss">
.border {
  background-color: #1ea3de;
  min-height: 40px;
  box-sizing: border-box;
}
nav {
  color: white;
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
    height: 2em;
    border: 1px solid #ffffff81;
    background-color: #005870;
    border-radius: 10px;
    overflow: hidden;
    #progress {
      height: 100%;
      background-color: #bbcf3e;
    }
  }

  .heading {
    grid-area: b;
    margin: 0% 2%;
    align-self: center;
    #heading-title {
      font-size: 17px;
      letter-spacing: 5px;
      font-weight: bold;
      text-transform: uppercase;
    }
    #heading-subtitle {
      font-weight: bold;
      color: #f5d755;
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
    .btn-med {
      width: 100%;
      &:hover {
        cursor: pointer;
      }
    }
  }
}
</style>
