<template>
  <div class="flex flex-col md:flex-row fullscreen">
    <div class="w-full md:w-3/4 container px-2 py-8">
      <div class="flex items-center justify-between mb-6">
        <h1 class="font-semibold text-lg">Stocks</h1>
        <button class="btn btn-outline text-sm block" @click.prevent="toggle">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
            <path
              class="heroicon-ui"
              d="M5 3h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5c0-1.1.9-2 2-2zm0 2v4h4V5H5zm10-2h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2V5c0-1.1.9-2 2-2zm0 2v4h4V5h-4zM5 13h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4c0-1.1.9-2 2-2zm0 2v4h4v-4H5zm10-2h4a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2v-4c0-1.1.9-2 2-2zm0 2v4h4v-4h-4z"
            ></path>
          </svg>
          <span v-if="!openToggle">Open</span>
          <span v-else>Close</span>
        </button>
      </div>
      <div class="flex flex-wrap -mx-2">
        <Card v-for="stock in stocks" :stock="stock" :key="stock.name" types="buy"/>
      </div>
    </div>
    <Sidebar :show="openToggle" type="portfolio"/>
  </div>
</template>
<script>
import Stock from "./Stock.vue";
import Card from "../Card.vue";
import Sidebar from "../Sidebar.vue";

export default {
  components: {
    Card,
    Stock,
    Sidebar
  },
  data() {
    return {
      openToggle: false
    };
  },
  methods: {
    toggle() {
      this.openToggle = !this.openToggle;
    }
  },
  computed: {
    stocks() {
      return this.$store.getters.stocks;
    }
  }
};
</script>

<style>
.fullscreen {
  height: calc(100vh - 60px);
}
</style>
