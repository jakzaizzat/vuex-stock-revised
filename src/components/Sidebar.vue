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


<style scoped>
.sidebar {
  background-color: #2d3748;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.sidebar h2 {
  color: #fff;
  font-weight: 600;
  margin-bottom: 1rem;
  font-size: 1.25rem;
}

.sidebar ul {
  list-style-position: inside;
}

.sidebar ul li {
  color: #edf2f7;
  margin-bottom: 1rem;
}
</style>
