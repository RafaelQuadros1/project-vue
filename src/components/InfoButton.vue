<template>
  <button class="info-button" @click="showInfo">
    <BookAlert class="icon-info" />
  </button>

  <div v-bind:aria-modal="infoVisible">
    <transition name="fade">
      <div v-if="infoVisible" class="info-modal">
        <h2>About This App</h2>
        <p>This is a simple clicker app built with Vue.js.</p>
        <p>Click the button to increase your score!</p>
      </div>
    </transition>
  </div>
</template>

<script>
import { BookAlert } from "lucide-vue-next";

export default {
  name: "InfoButton",
  components: {
    BookAlert,
  },

  data() {
    return {
      infoVisible: false,
    };
  },

  methods: {
    showInfo() {
      this.infoVisible = !this.infoVisible;
    },
  },
  watch: {
    infoVisible(newValue) {
      if (newValue) {
        document.body.style.overflow = "hidden"; // Prevent scrolling when modal is open
      } else {
        document.body.style.overflow = ""; // Restore scrolling when modal is closed
      }
    },
  },
};
</script>

<style>
.info-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: transparent;
  border: none;
  border-radius: 50%;
  padding: 7px;
}

.info-modal {
  position: fixed;
  bottom: 20%;
  right: 20px;
  transform: translate(0%, 50%);
  background-color: white;
  box-shadow: 0 2px 7px rgba(0, 0, 0, 0.6);
  border-radius: 5px;
  padding: 20px;
  z-index: 1000;
}

.icon-info {
  width: 24px;
  height: 24px;
  color: #4a5568; /* Cor do ícone no modo claro */
}

.icon-info:hover {
  color: #fbbf24; /* Cor do ícone ao passar o mouse */
  cursor: pointer;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.dark .info-modal {
  background-color: #181818; /* Cor do fundo no modo escuro */
  color: #f7fafc; /* Cor do texto no modo escuro */
  border: 1px solid #42b983; /* Borda no modo escuro */
}

.dark .info-button {
  color: #f7fafc; /* Cor do ícone no modo escuro */
}

.dark .icon-info {
  color: #fbbf24; /* Cor do ícone no modo escuro */
}

.dark .icon-info:hover {
  color: #f7fafc; /* Cor do ícone ao passar o mouse no modo escuro */
  cursor: pointer;
}


</style>
