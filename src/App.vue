<!--
 * @Author: xuxing
 * @Github: 
 * @Date: 2022-02-07 15:30:07
 * @LastEditors: xuxing
 * @LastEditTime: 2022-03-02 11:45:10
 * @Description: 
-->
<template>
  <Split />
</template>

<script>
import Split from './components/Split.vue';

export default {
  name: 'App',
  components: {
    Split
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: aquamarine;
}
</style>
