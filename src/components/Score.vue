<template>
  <div class="score">
    <MousePointerClick class="icon-score" />
    <h2 v-if="count > 0">{{ count }}</h2>
    <h2 v-else>00</h2>
  </div>
</template>

<script>
import { useStorage } from '@vueuse/core'
import { MousePointerClick } from 'lucide-vue-next';

const count = useStorage('clickCount', 0);

export default {
  name: 'Score',
    components: {
        MousePointerClick,
    },
  setup() {
    return {
      count,
    };
  },
};


</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Orbitron:wght@400..900&display=swap");


.score {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-family: 'Orbitron', sans-serif;
  color: #fbbf24; /* Cor do texto no modo claro */
}

h2 {
  font-family: 'Orbitron', sans-serif;
  font-size: 1rem;
  color: #4a5568; /* Cor do texto no modo claro */
}

.icon-score {
  width: 1.5rem;
  height: 1.5rem;
  color: #fbbf24; /* Cor do ícone no modo claro */
}

.dark .score {
  color: #fbbf24; /* Cor do texto no modo escuro */
}
.dark h2 {
  color: #ffffff; /* Cor do texto no modo escuro */
}

</style>