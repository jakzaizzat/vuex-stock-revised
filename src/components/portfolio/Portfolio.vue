<template>
  <div class="flex flex-col md:flex-row fullscreen">
    <div class="w-full md:w-3/4 container px-2 py-8">
      <div class="flex items-center justify-between mb-6">
        <h1 class="font-semibold text-lg">Portfolio ~ {{ total | currency }}</h1>
        <SidebarToggle v-model="openToggle"/>
      </div>
      <div class="flex flex-wrap -mx-2" v-if="stocks.length">
        <Card v-for="stock in stocks" :stock="stock" :key="stock.name" types="sell"></Card>
      </div>
      <Empty v-else/>
    </div>
    <Sidebar :show="openToggle" type="stock"/>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import Stock from "./Stock.vue";
import Card from "../Card.vue";
import Sidebar from "../Sidebar.vue";
import SidebarToggle from "../SidebarToggle.vue";
import Empty from "../Empty.vue";

export default {
  computed: {
    ...mapGetters({ stocks: "portfolio" }),
    total() {
      var total = 0;
      this.stocks.forEach(stock => {
        total += stock.price * stock.quantity;
      });
      return total;
    }
  },
  components: {
    Stock,
    Card,
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
  }
};
</script>