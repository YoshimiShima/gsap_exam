<script setup lang="ts">

import { gsap } from 'gsap';
import { useDraggable } from '@vueuse/core'

const el = ref<HTMLElement | null>(null)
const {position, style } = useDraggable(el, {
  initialValue: { x: 200, y: 200 },
})

const points = [
  { x: 87, y: 245 },
  { x: 276, y: 87 },
  { x: 924, y: 87 },
  { x: 1088, y: 245 },
  { x: 1088, y: 590 },
  { x: 924, y: 753 },
  { x: 276, y: 753 },
  { x: 87, y: 590 },
]

const mouseUp = () => {
  const { x, y } = position.value

  const nearestPoint = points.reduce((prev, curr) => {
    const prevDistance = Math.sqrt((prev.x - x) ** 2 + (prev.y - y) ** 2)
    const currDistance = Math.sqrt((curr.x - x) ** 2 + (curr.y - y) ** 2)
    return prevDistance < currDistance ? prev : curr
  })

  if (Math.sqrt((nearestPoint.x - x) ** 2 + (nearestPoint.y - y) ** 2) <= 80) {
    gsap.to(position.value, {
      x: nearestPoint.x,
      y: nearestPoint.y,
      ease: 'power4.out',
      duration: 0.5,
    })
  }
}

watch(position, (newValue, oldValue) => {
  const { x, y } = newValue
  const nearestPoint = points.reduce((prev, curr) => {
    const prevDistance = Math.sqrt((prev.x - x) ** 2 + (prev.y - y) ** 2)
    const currDistance = Math.sqrt((curr.x - x) ** 2 + (curr.y - y) ** 2)
    return prevDistance < currDistance ? prev : curr
  })

  if (Math.sqrt((nearestPoint.x - x) ** 2 + (nearestPoint.y - y) ** 2) <= 80) {
    position.value.x = nearestPoint.x
    position.value.y = nearestPoint.y
  }
})

</script>

<template>
<div class = "box">
  <div class = "screen">
    <div ref="el" :style="style" style="position: fixed" @mouseup="mouseUp">
      <div class="button"></div>
    </div>
  </div>
</div>

</template>

<style>
.box {
  border: 80px groove #2f3437;
  border-radius: 30px;
  background-color: rgba(29, 29, 27, 0.339);
  width: 1062px;
  height: 730px;
  margin-right: auto
}

.button {
  bottom: 20px;
  right: 20px;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: #4a47476a;
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
