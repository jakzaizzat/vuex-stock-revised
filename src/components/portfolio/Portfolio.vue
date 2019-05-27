<template>
  <div class="px-2 py-8">
    <!-- <Stock v-for="stock in stocks" :stock="stock"></Stock> -->
    <div class="flex flex-wrap -mx-2">
      <Card v-for="stock in stocks" :stock="stock" :key="stock.name" types="sell"></Card>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import Stock from "./Stock.vue";
import Card from "../Card.vue";

export default {
  computed: {
    // assign state.portfolio to variable stocks
    ...mapGetters({ stocks: "portfolio" })
    // the above is the same as:
    // stocks() {
    //   return this.$store.getters.portfolio;
    // }
  },
  components: {
    Stock,
    Card
  }
};
</script>