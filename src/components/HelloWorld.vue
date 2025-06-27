<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <button class="btn" @click="handleClick">Click</button>

    <transition name="fade">
      <div v-if="NotificationVisible" class="notification">
        <p>
          {{ NotificationMessage }}
        </p>
        <button class="btn-notification" @click="NotificationVisible = false">
          X
        </button>
      </div>
    </transition>
  </div>
</template>

<script>
import { ref } from "vue";
import { useStorage } from "@vueuse/core";

export default {
  name: "HelloWorld",
  props: {
    msg: {
      type: String,
      default: "Welcome to your clicker app!",
    },
  },
  setup() {
    const count = useStorage("clickCount", 0);
    const NotificationVisible = ref(false);
    const NotificationMessage = ref("");
    let clickTimeout = null;

    function savecount() {
      useStorage("clickCount", count.value);
    }

    function showNotification(message) {
      NotificationMessage.value = message;
      NotificationVisible.value = true;
    }

    function xpThreshold(xp) {
      // Exemplo usando raiz quadrada multiplicada pra dar escala
      return Math.max(5, Math.floor(Math.sqrt(xp) * 1));
    }

    function handleClick() {
      count.value++;

      const threshold = xpThreshold(count.value);

      // Dispara notificação só se o número de cliques for múltiplo do threshold
      if (count.value % threshold === 0) {
        showNotification(
          `Você alcançou ${count.value} cliques! Próxima meta em +${threshold} cliques.`
        );
      }
      if (clickTimeout) clearTimeout(clickTimeout);
      clickTimeout = setTimeout(() => {
        NotificationVisible.value = false;
      }, 5000);
    }

    return {
      count,
      NotificationVisible,
      NotificationMessage,
      handleClick,
      savecount,
    };
  },
};
</script>


<style scoped>
.hello {
  text-align: center;
}

h1 {
  font-size: 3.5em;
  color: #42b983;
}

p {
  font-size: 1.2em;
  color: #35495e;
  padding: 20px;
}

a {
  color: #42b983;
}
a:hover {
  text-decoration: underline;
}

.btn {
  padding: 10px 20px;
  font-size: 1.2em;
  color: white;
  background-color: #42b983;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.notification {
  position: fixed;
  bottom: 20px;
  left: 20px;
  background-color: #f0f0f0;
  box-shadow: 0 2px 7px rgba(0, 0, 0, 0.6);
  border-left: #42b983 5px solid;
  border-radius: 5px;
  padding: 15px;
}

.notification p {
  margin: 0;
  padding-right: 30px; /* Space for the close button */
}

.btn-notification {
  padding: 5px 10px;
  font-size: 1em;
  color: white;
  background-color: #42b983;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  position: absolute;
  top: 5px;
  right: 5px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.dark .notification {
  background-color: #181818; /* Dark mode background */
  color: #0089e4; /* Light text color for dark mode */
  border-left: #42b983 5px solid; /* Green border */
}

.dark p {
  color: #f7fafc; /* Light text color for dark mode */
}

@media screen and (max-width: 600px) {
  h1 {
    font-size: 2em;
  }

  .notification {
    width: 70%;
    left: 5%;
    bottom: 10px;
  }
}
</style>