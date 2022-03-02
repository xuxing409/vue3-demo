
<template>
  <!-- <h2>{{width}}</h2>
  <h2>{{size}}</h2>
  <h2>{{offset}}</h2>-->
  <div class="split-pane-wrapper" ref="aplitPanref">
    <div class="pane-left" :style="{right: anotherOffset}"></div>
    <div class="split-pane-line" @mousedown="mousedown" :style="{left: offset}"></div>
    <div class="pane-right" :style="{left:offset}"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
const offset = ref('50%');

const anotherOffset = ref('50%');

const startX = ref(0);
const offsetLeft = ref(0);
const innerX = ref(0);
const width = ref(0);

const size = ref(0);
const aplitPanref = ref(null);

let isMoving = false;

const px2percent = (numerator, denominator) => {
  return parseFloat(numerator) / parseFloat(denominator);
};

onMounted(() => {
  console.log(aplitPanref);
  size.value = aplitPanref.value.offsetWidth;
});

const mousemove = e => {
  if (isMoving) {
    width.value = e.pageX - startX.value;
    +offsetLeft.value;
    let changeValue = px2percent(offsetLeft.value + width.value, size.value);
    if (0 < changeValue && changeValue < 1) {
      offset.value = changeValue * 100 + '%';
      anotherOffset.value = (1 - changeValue) * 100 + '%';
    }
  }
};

const mousedown = e => {
  document.addEventListener('mousemove', mousemove);
  document.addEventListener('mouseup', mouseup);
  offsetLeft.value = e.target.offsetLeft;
  startX.value = e.pageX;
  innerX.value = offsetLeft.value - startX.value;

  isMoving = true;
};
const mouseup = e => {
  console.log(e);
  isMoving = false;
  document.removeEventListener('mousemove', () => {});
  document.removeEventListener('mouseup', () => {});
};
</script>

<style>
.split-pane-wrapper {
  width: 400px;
  height: 400px;
  box-sizing: border-box;
  position: relative;
  margin-left: 100px;
  border: 1px solid #eee;
}
.pane-left {
  left: 0;
  top: 0;
  bottom: 0;
  height: 100%;
  display: inline-block;
  background-color: red;
  position: absolute;
}
.pane-right {
  right: 0;
  top: 0;
  bottom: 0;
  height: 100%;
  display: inline-block;
  background-color: green;
  position: absolute;
}
.split-pane-line {
  display: inline-block;
  width: 10px;
  height: 100%;
  left: 100px;
  background-color: #eee;
  position: absolute;
  z-index: 10;
  transform: translate(-50%, 0);
}
.split-pane-line:hover {
  cursor: col-resize;
}
</style>
