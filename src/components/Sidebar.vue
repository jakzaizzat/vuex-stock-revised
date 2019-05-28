<template>
  <div class="w-full md:w-1/4 sidebar" v-show="show">
    <div v-if="type === 'portfolio'">
      <h2>Portfolio</h2>

      <ul>
        <li v-for="stock in ownStocks" :key="stock.id" class="flex items-center justify-between">
          <div class="text-sm">
            <p>{{ stock.name }}</p>
            <p class="text-gray-100">{{ stock.price | currency }}</p>
          </div>
          <span class="text-lg font-semibold text-white">{{ stock.quantity }}</span>
        </li>
      </ul>
    </div>

    <div v-else>
      <h2>Stock</h2>

      <ul>
        <li v-for="stock in stocks" :key="stock.id" class="flex items-center justify-between">
          <div class="text-sm">
            <p>{{ stock.name }}</p>
            <p class="text-gray-100">{{ stock.price | currency }}</p>
          </div>
          <span class="text-lg font-semibold text-white">{{ stock.quantity }}</span>
        </li>
      </ul>
    </div>

    <drop
      class="sidebar__drag"
      @drop="handleDrop"
      :class="{ active }"
      @dragover="active = true"
      @dragleave="active = false"
    >
      <span>Drag stock over here</span>
    </drop>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  props: {
    show: {
      required: true,
      type: Boolean
    },
    type: {
      required: true,
      type: String
    }
  },
  data() {
    return {
      active: false
    };
  },
  computed: {
    ...mapGetters({ ownStocks: "portfolio" }),

    stocks() {
      return this.$store.getters.stocks;
    }
  },
  methods: {
    handleDrop(data, event) {
      this.active = false;
      alert(`You dropped with data: ${JSON.stringify(data)}`);
    }
  }
};
</script>


<style lang="postcss" scoped>
.sidebar {
  @apply bg-gray-800 p-4 flex flex-col justify-between;
}

.sidebar h2 {
  @apply text-white font-semibold mb-4 text-xl;
}

.sidebar ul {
  @apply list-inside;
}

.sidebar ul li {
  @apply text-gray-200 mb-4;
}

.sidebar__drag {
  @apply bg-gray-700 h-32 w-auto rounded shadow-inner flex items-center justify-center;
}

.sidebar__drag.active {
  @apply bg-black;
}

.sidebar__drag span {
  @apply text-gray-400;
}
</style>
