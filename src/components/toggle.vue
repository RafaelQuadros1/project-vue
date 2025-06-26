<template>
  <button class="toggle" @click="toggleDarkMode">
    <Sun class="icon" v-if="isDarkMode" />
    <Moon class="icon-moon" v-else />
  </button>
</template>

<script setup>
import { useStorage } from "@vueuse/core";
import {Sun, Moon} from 'lucide-vue-next'

const isDarkMode = useStorage("theme", false);

// Sempre aplica a classe ao iniciar
if (isDarkMode.value) {
  document.documentElement.classList.add("dark");
} else {
  document.documentElement.classList.remove("dark");
}

function toggleDarkMode() {
  isDarkMode.value = !isDarkMode.value;

  document.documentElement.classList.toggle("dark", isDarkMode.value);
}
</script>


<style scoped>
.toggle {
  background-color: transparent;
  color: #4a5568; /* Cor do ícone no modo claro */
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
  font-size: 1rem;
}

.icon {
  width: 24px;
  height: 24px;
}

.dark .toggle {
  color: #fbbf24; /* Cor do ícone no modo escuro */
}

.icon-moon {
  color: #4a5568; /* Cor do ícone no modo claro */
}

</style>