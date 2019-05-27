<template>
  <div class="flex">
    <div class="w-3/4 container px-2 py-8">
      <button class="btn btn-outline ml-auto block mb-2">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
          <path
            class="heroicon-ui"
            d="M5 3h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5c0-1.1.9-2 2-2zm0 2v4h4V5H5zm10-2h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2V5c0-1.1.9-2 2-2zm0 2v4h4V5h-4zM5 13h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4c0-1.1.9-2 2-2zm0 2v4h4v-4H5zm10-2h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2v-4c0-1.1.9-2 2-2zm0 2v4h4v-4h-4z"
          ></path>
        </svg>
        Open
      </button>
      <div class="flex flex-wrap -mx-2">
        <!-- <Stock v-for="stock in stocks" :stock="stock" :key="stock.name"></Stock> -->
        <Card v-for="stock in stocks" :stock="stock" :key="stock.name" types="buy"/>
      </div>
    </div>
    <div class="w-1/4 sidebar">
      <div>
        <h2>Portfolio</h2>

        <ul>
          <li>Google @$1200</li>
          <li>Google @$1200</li>
        </ul>
      </div>

      <div class="sidebar__drag"></div>
    </div>
  </div>
</template>
<script>
import Stock from "./Stock.vue";
import Card from "../Card.vue";
export default {
  components: {
    Card,
    Stock
  },
  computed: {
    stocks() {
      return this.$store.getters.stocks;
    }
  }
};
</script>

<style lang="postcss">
.sidebar {
  height: calc(100vh- 3.75rem);
  @apply bg-gray-800 p-4 flex flex-col justify-between;
}

.sidebar h2 {
  @apply text-white font-semibold mb-4;
}

.sidebar ul {
  @apply list-inside;
}

.sidebar ul li {
  @apply text-gray-200 mb-2;
}

.sidebar__drag {
  @apply bg-gray-700 h-32 w-auto rounded shadow-inner;
}
</style>
