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
      <h2>Available Stock</h2>

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
    <SidebarDrop :type="type"/>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

import SidebarDrop from "../components/SidebarDrop.vue";
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
  components: {
    SidebarDrop
  },
  data() {
    return {
      active: false
    };
  },
  computed: {
    ...mapGetters({ ownStocks: "portfolio" }),
    funds() {
      return this.$store.getters.funds;
    },
    stocks() {
      return this.$store.getters.stocks;
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
</style>
