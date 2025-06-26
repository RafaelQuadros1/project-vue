<template>
  <div class="score">
    <MousePointerClick />
    <h2>{{ count }}</h2>
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
  color: #ffffff;
}

</style>