<template>
  <button class="toggle" @click="toggleDarkMode">
    {{ isDarkMode ? "on" : "of" }}
  </button>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isDarkMode = ref(false);

function toggleDarkMode() {
  isDarkMode.value = !isDarkMode.value;

  if (isDarkMode.value) {
    document.documentElement.classList.add("dark");
  } else {
    document.documentElement.classList.remove("dark");
  }
}

// Se quiser, pode iniciar baseado no tema do sistema
onMounted(() => {
  if (
    window.matchMedia &&
    window.matchMedia("(prefers-color-scheme: dark)").matches
  ) {
    isDarkMode.value = true;
    document.documentElement.classList.add("dark");
  }
});
</script>


<style scoped>
.toggle {
  padding: 0.5rem 1rem;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
  font-size: 1rem;
}
.toggle:hover {
  background-color: #36a65f;
}
</style>