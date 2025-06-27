<template>
  <button class="info-button" @click="showInfo">
    <BookAlert class="icon-info" />
  </button>

  <div v-bind:aria-modal="infoVisible">
    <transition name="fade">
      <div v-if="infoVisible" class="info-modal">
        <h2>About this project</h2>
        <p>
          This project was created to demonstrate the use of the Vue framework
          in a practical way.
        </p>
        <p>If you encounter any issues, feel free to contact the developer.</p>
        <p>
          by:
          <a href="https://github.com/RafaelQuadros1">Rafael Quadros</a>
        </p>
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
        document.body.style.overflow = "hidden";
      } else {
        document.body.style.overflow = "";
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
  bottom: 10%;
  right: 1.5%;
  /* transform: translate(0%, 50%); */
  background-color: white;
  border-radius: 5px;
  border: 1px solid #42b983;
  padding: 20px;
  z-index: 1000;
  width: 300px;
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

@media screen and (max-width: 600px) {
  .info-modal {
    width: 80%;
    right: 5%;
    bottom: 10%;
  }
  
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
