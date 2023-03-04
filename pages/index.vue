<script setup lang="ts">

import { gsap } from 'gsap';
import { useDraggable } from '@vueuse/core'

const el = ref<HTMLElement | null>(null)
const { x, y, position, style } = useDraggable(el, {
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
    <div class="button">{{ Math.round(position.value.x) }}, {{ Math.round(position.value.y) }}</div>
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

// })
//       { x: 187, y: 120 },
//       { x: 296, y: 29 },
//       { x: 1199, y: 29 },
//       { x: 1324, y: 120 },
//       { x: 1324, y: 644 },
//       { x: 1199, y: 767 },
//       { x: 296, y: 767 },
//       { x: 187, y: 644 }

