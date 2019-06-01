<template>
  <div class="flex flex-col md:flex-row fullscreen">
    <div class="w-full md:w-3/4 container px-2 py-8">
      <div class="flex items-center justify-between mb-6">
        <h1 class="font-semibold text-lg">Portfolio ~ {{ total | currency }}</h1>
        <SidebarToggle v-model="openToggle"/>
      </div>
      <div class="flex flex-wrap -mx-2" v-if="stocks.length">
        <Stock v-for="stock in stocks" :stock="stock" :key="stock.name" types="sell"/>
      </div>
      <Empty v-else/>
    </div>
    <Sidebar :show="openToggle" type="stock"/>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import Stock from "../components/Stock.vue";
import Sidebar from "../components/Sidebar.vue";
import SidebarToggle from "../components/SidebarToggle.vue";
import Empty from "../components/Empty.vue";

export default {
  components: {
    Stock,
    Sidebar,
    SidebarToggle,
    Empty
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
    ...mapGetters({ stocks: "portfolio" }),
    total() {
      var total = 0;
      this.stocks.forEach(stock => {
        total += stock.price * stock.quantity;
      });
      return total;
    }
  }
};
</script>