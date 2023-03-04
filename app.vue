<script setup lang="ts">

import { gsap } from 'gsap';
import { useDraggable } from '@vueuse/core'

const el = ref<HTMLElement | null>(null)
const { position, style } = useDraggable(el, {
  initialValue: { x: 200, y: 200 },
})

const initialPosition = { x: 200, y: 200 }

const mouseUp = () => {
  const { x, y } = position.value
  if (x === initialPosition.x && y === initialPosition.y) {
    return
  }
  gsap.to(position.value, {
    x: initialPosition.x,
    y: initialPosition.y,
    ease: 'back',
    duration: 0.5,
  })
}

</script>

<template>
<div class = "image">
  <div ref="el" :style="style" style="position: fixed" @mouseup="mouseUp">
    <div class="button"></div>
  </div>
</div>

</template>

<style>
.image {
  border: 20px groove #0a486c;
  width: 1200px;
  height: 800px;
  margin:0 auto
}
.button {
  bottom: 20px;
  right: 20px;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: #726d6d6a;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.button::before {
  content: "";
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #fff;
}
</style>





<!-- <script setup lang="ts">
import { gsap } from 'gsap';

onMounted(() => {
  const circles = document.querySelectorAll('.circle');
  gsap.fromTo(circles,
    { y: -30 },
    { y: 30,
      ease: "power1.inOut", // 進行具合
      stagger: {
        each: 0.15, // アニメーション間の時間
        repeat: -1, // 無限に繰り返し
        yoyo: true  // アニメーションの反復
      }
  });
});

</script>

<template>
<div class="circle"></div>
<div class="circle"></div>
<div class="circle"></div>
</template>

<style>
body {
  background: #000000;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.circle {
  background: #ffffff;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin: 10px;
}


</style> -->
