
<template>
  <div>
    {{props.foo}}
    <button @click="childClick">子组件按钮</button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
const props = defineProps({
  foo: String
});
const emit = defineEmits(['child']);
const childClick = () => {
  emit('child', 'childClick');
};
</script>

<style>
</style>
