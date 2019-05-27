<template>
  <div class="px-2 py-8">
    <div class="flex flex-wrap -mx-2">
      <!-- <Stock v-for="stock in stocks" :stock="stock" :key="stock.name"></Stock> -->
      <Card v-for="stock in stocks" :stock="stock" :key="stock.name"/>
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