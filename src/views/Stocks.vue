<template>
  <div class="flex flex-col md:flex-row fullscreen">
    <div class="w-full md:w-3/4 container px-2 py-8">
      <div class="flex items-center justify-between mb-6">
        <h1 class="font-semibold text-lg">Stocks</h1>
        <SidebarToggle v-model="openToggle"/>
      </div>
      <div class="flex flex-wrap -mx-2">
        <Stock v-for="stock in stocks" :stock="stock" :key="stock.name" types="buy"/>
      </div>
    </div>
    <Sidebar :show="openToggle" type="portfolio"/>
  </div>
</template>
<script>
import Stock from "../components/Stock.vue";
import Sidebar from "../components/Sidebar.vue";
import SidebarToggle from "../components/SidebarToggle.vue";

export default {
  components: {
    Stock,
    Sidebar,
    SidebarToggle
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
