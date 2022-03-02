
<template>
  <div
    class="scroll-container"
    :style="{
      transform: `translate3d(0px, ${-scroll}px, 0px)`
    }"
  >
    <div
      class="scroll-item"
      v-for="item,index of dataOrigin"
      :key="item+index"
      :style="{ height: itemHeight + 'px' }"
    >{{ item +String(item)}}</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// export default {
// setup() {
const dataOrigin = ref([1, 2, 3, 4, 5, 6, 7, 8, 9]);
const itemHeight = 80;
const scroll = ref(0);
const setItem = () => {
  dataOrigin.value.push(dataOrigin.value[0]);
};

const removeItem = () => {
  dataOrigin.value = dataOrigin.value.filter((item, index) => index !== 0);
};

const autoScroll = () => {
  setItem();

  setInterval(() => {
    scroll.value++;
    if (scroll.value === itemHeight) {
      scroll.value = 0;
      removeItem();
      setItem();

      console.log(dataOrigin.value);
    }
  }, 30);
};

onMounted(() => {
  autoScroll();
});

// return {
//   scroll,
//   dataOrigin,
//   itemHeight
// }
// }
// }
</script>

<style scoped>
.scroll-container {
  width: 100%;
  height: 100%;
}
.scroll-item {
  /* height: 80px; */
  line-height: 80px;
  text-align: center;
  border-bottom: 1px solid #ddd;
  box-sizing: border-box;
}
</style>
