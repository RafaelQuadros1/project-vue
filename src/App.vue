<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import Infobutton from "./components/InfoButton.vue";
import Score from "./components/Score.vue";
import Shop from "./components/shop.vue";
import Toggle from "./components/Toggle.vue";
</script>

<template>
  <div>
    <nav class="navbar">
      <Score />
      <Toggle />
    </nav>
    <main>
      <HelloWorld :msg="message" />
    </main>
    <footer>
      <Shop />
      <Infobutton />
    </footer>
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #f5f5f5;
  line-height: 1.6;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
