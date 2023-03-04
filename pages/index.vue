<script setup lang="ts">
import { gsap } from 'gsap';
import { useDraggable } from '@vueuse/core'
import {
  AppleAlt,
  ApplePay,
  MailBulk,
  Phone,
  Line,
  Amazon,
  StarRegular
} from '@vicons/fa'

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
      duration: 0.8,
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
});

// const menuBox = ref(null)
// const onDoubleClickMethod = (event) => {
//   if(event.detail === 2) {
//     const menuBoxElement = menuBox.value
//     if (menuBoxElement) {
//       menuBoxElement.style.visibility = 'visible'
//     }
//   }
// }
// const close = () => {
//   const menuBoxElement = menuBox.value
//   if (menuBoxElement) {
//     menuBoxElement.style.visibility = 'hidden'
//   }
// }

const menuBox = ref(null)
const popUp = () => {
  const menuBoxElement = menuBox.value
  if (menuBoxElement) {
    gsap.to(menuBoxElement, {
      duration: 0.5,
      opacity: 1,
      scale: 1,
      visibility: 'visible'
    })
  }
}

const popOut = () => {
  const menuBoxElement = menuBox.value
  if (menuBoxElement) {
    gsap.to(menuBoxElement, {
      duration: 0.5,
      opacity: 0,
      scale: 0.5,
      onComplete: () => {
        menuBoxElement.style.visibility = 'hidden'
      }
    })
  }
}

const onDoubleClickMethod = (event) => {
  if(event.detail === 2) {
    popUp()
  }
}

const close = () => {
  popOut()
}

</script>

<template lang="pug">
.box
  .screen
    div(ref='el', :style='style', style='position: fixed', @mouseup='mouseUp', @mousedown='onDoubleClickMethod')
      .button
  .menuBox(ref='menuBox')
    Phone(width="60px" height="60px")
    ApplePay(width="60px" height="60px")
    MailBulk(width="60px" height="60px")
    Line(width="60px" height="60px")
    Amazon(width="60px" height="60px")
    AppleAlt(width="60px" height="60px")
    .iconButton(@click="close")
      StarRegular(width="60px" height="60px")
      span.buttonText Close
</template>

<style>
.box {
  border: 80px groove #2f3437;
  border-radius: 30px;
  background-color: rgba(29, 29, 27, 0.339);
  width: 1062px;
  height: 730px;
  margin-right: auto;
  position: relative;
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
.menuBox{
  border: none;
  border-radius: 40px;
  background-color: rgba(12, 12, 11, 0.659);
  width: 400px;
  height: 360px;
  position:absolute;
  margin: 185px 0 0 331px;
  visibility: hidden;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
.menuBox > * {
  flex: 1 0 25%;
  text-align: center;
  padding: 10px;
  font-size: 8px;
  color: #fff;
}
.menuBox svg path{
  fill: rgba(246, 242, 242, 0.902);
}

</style>
