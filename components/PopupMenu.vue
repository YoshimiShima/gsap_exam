<script setup lang="ts">
const onDoubleClickMethod = () => {
  const menuBoxElement = menuBox.value
  if (menuBoxElement) {
    menuBoxElement.style.visibility = 'visible'
  }
}
</script>

<template lang="pug">
.box
  .screen
    div(ref='el', :style='style', style='position: fixed', @mouseup='mouseUp', @mousedown='onDoubleClickMethod')
      .button
        .menuBox(ref='menuBox')

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
  background-color: rgba(8, 8, 7, 0.543);
  width: 400px;
  height: 360px;
  position:absolute;
  margin: 185px 0 0 331px;
  visibility: hidden;
}
</style>
