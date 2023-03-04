<script setup lang="ts">
import { gsap } from 'gsap';

const el = ref<HTMLElement | null>(null)
const { x, y, style } = useDraggable(el, {
  initialValue: { x: 200, y: 200 },
})

</script>


<template>
<div class = "image">
  <div ref="el" :style="style" style="position: fixed">
    <div class="button">{{ Math.round(x) }}, {{ Math.round(y) }}</div>
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