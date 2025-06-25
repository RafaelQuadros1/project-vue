<script setup>
import HelloWorld from './components/HelloWorld.vue'

</script>

<template>
  <div>
    <HelloWorld :msg="message" />
  </div>
</template>

<style scoped>

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #f5f5f5;
  line-height: 1.6;
}
</style>
