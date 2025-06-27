<template>
  <button class="btn-shop" @click="handleClick">
    <ShoppingBag class="icon-info" />
  </button>

  <div v-bind:aria-modal="shopVisible">
    <transition name="fade">
      <div v-if="shopVisible" class="shop-modal">
        <nav class="shop-nav">
          <Score />
          <h2 class="shop-title">shop-clicaí</h2>
          <button class="btn-close" @click="handleClick">
            <X />
          </button>
        </nav>
        <div class="shop-content">
          <div>
            <ul class="shop-list">
              <li class="shop-item" v-for="item in itens" :key="item.name">
                {{ item.name }} - <BanknoteArrowUp />
                {{ item.price }}
                <!-- buttom de compra -->
                <button
                  class="btn-compra"
                  @click="handlecompraClick(item)"
                  :disabled="clickCount < item.price"
                >
                  Comprar
                </button>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { BanknoteArrowUp, ShoppingBag } from "lucide-vue-next";
import Score from "./Score.vue";
import { X } from "lucide-vue-next";
import { useStorage } from "@vueuse/core";

export default {
  components: {
    ShoppingBag,
    Score,
    X,
    BanknoteArrowUp,
  },
  data() {
    return {
      shopVisible: false,
      itens: [
        { name: "Item 1", price: 100 },
        { name: "Item 2", price: 200 },
        { name: "Item 3", price: 300 },
      ],
    };
  },
  methods: {
    handleClick() {
      this.shopVisible = !this.shopVisible;
    },
  },
  watch: {
    shopVisible(newValue) {
      if (newValue) {
        document.body.style.overflow = "hidden";
      } else {
        document.body.style.overflow = "";
      }
    },
  },

  setup() {
    const clickCount = useStorage("clickCount", 0);

    function handlecompraClick(item) {
      if (clickCount.value >= item.price) {
        clickCount.value -= item.price;
        alert(`Você comprou: ${item.name}!`);
      } else {
        alert("Você não tem cliques suficientes para comprar este item!");
      }
    }

    return {
      handlecompraClick,
      clickCount,
    };
  },
};
</script>

<style>
.btn-shop {
  position: fixed;
  bottom: 20px;
  left: 20px;
  background-color: transparent;
  border: none;
  border-radius: 50%;
  padding: 7px;
}

.shop-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
  border-bottom: 1px solid #42b983; /* Light mode border */
}

.icon-info {
  width: 24px;
  height: 24px;
  color: #4a5568; /* Light mode icon color */
}

.shop-modal {
  position: fixed;
  bottom: 10%;
  left: 1.5%;
  background-color: #fff; /* Light mode background */
  color: #2c3e50; /* Light mode text color */
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #42b983;
  z-index: 1000;
  width: 600px;
  height: 500px;
}

.btn-close {
  top: 10px;
  right: 10px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  font-size: 1rem;
}

.btn-compra:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.shop-content {
  margin-top: 20px;
  font-size: 1.2rem;
}

.shop-list {
  list-style: none;
  padding: 0;
}

.shop-item {
  margin-bottom: 10px;
}

.shop-title {
  font-size: 1.5rem;
  margin-bottom: 10px;
  text-align: center;
}

@media screen and (max-width: 600px) {
  .shop-modal {
    width: 80%;
    left: 5%;
    bottom: 10%;
  }
}

.dark .btn-close {
  color: #f7fafc; /* Dark mode close button color */
}

.dark .btn-shop {
  background-color: transparent;
  color: #fbbf24; /* Dark mode icon color */
}

.dark .shop-modal {
  background-color: #181818; /* Dark mode background */
  color: #f5f5f5; /* Dark mode text color */
  border: 1px solid #42b983;
}
</style>