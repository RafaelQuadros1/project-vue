<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import toggle from "./components/toggle.vue";
import Infobutton from "./components/InfoButton.vue";
import score from "./components/score.vue";
</script>

<template>
  <div>
    <nav class="navbar">
      <score />
      <toggle />
    </nav>
    <main>
      <HelloWorld :msg="message" />
    </main>
    <footer>
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
