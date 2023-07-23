<script setup lang="ts">
import { reactive, shallowRef } from 'vue'
import { useAnimate, type MaybeElement } from '@vueuse/core'
import GlassShoes from './assets/27161639_m.jpg'
import GlassShoesFront from './assets/27161639_m_front.png'

const el = shallowRef<MaybeElement>()

const {
  play,
  pause,
  reverse,
  finish,
  cancel,
  startTime,
  currentTime,
  playbackRate,
  playState,
  replaceState,
  pending,
} = useAnimate(
  el,
  [
    { clipPath: 'circle(8% at 0% 30%)' },
    { clipPath: 'circle(25% at 50% 90%)' },
    { clipPath: 'circle(3% at 100% 30%)' },
    { clipPath: 'circle(15% at 0% 70%)' },
  ],
  {
    duration: 6000,
    iterations: 5,
    direction: 'alternate',
    easing: 'cubic-bezier(0.46, 0.03, 0.52, 0.96)',
  },
)
</script>

<template>
  <div class="info">
    startTime: {{ startTime }}<br>
    currentTime: {{ currentTime }}<br>
    playbackRate: {{ playbackRate }}<br>
    playState: {{ playState }}<br>
    replaceState: {{ replaceState }}<br>
    pending: {{ pending }}
  </div>
  <div class="wrapper">
    <div class="image">
      <img class="glass-shoes glass-shoes--base" :src="GlassShoes" alt="ガラスのシューズ">
      <img ref="el" class="glass-shoes glass-shoes--front" :src="GlassShoesFront" alt="ガラスのシューズ">
    </div>
    <div class="buttons">
      <button class="buttons__button" @click="play">Play</button>
      <button class="buttons__button" @click="pause">Pause</button>
      <button class="buttons__button" @click="reverse">Reverse</button>
      <button class="buttons__button" @click="finish">Finish</button>
      <button class="buttons__button" @click="cancel">Cancel</button>
    </div>
  </div>
</template>


<style>
body {
  background-color: #bbb;
}

.wrapper {
  display: grid;
  place-items: center;
  height: 100dvh;
}

.image {
  width: 700px;
  max-width: 100%;
  position: relative;
  overflow: hidden;
  border-radius: 20px;
}

.glass-shoes {
  width: 100%;
}

.glass-shoes--base {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  filter: brightness(0.2);
}

.glass-shoes--front {
  position: relative;
  z-index: 10;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.buttons__button {
  background-color: #1a9529;
  color: white;
  font-size: 18px;
  padding: 10px 14px;
  border-radius: 8px;
  appearance: none;
  border: none;
}

.info {
  position: fixed;
  width: 350px;
  top: 16px;
  right: 16px;
  background-color: white;
  border-radius: 16px;
  padding: 20px;
  z-index: 50;
}
</style>