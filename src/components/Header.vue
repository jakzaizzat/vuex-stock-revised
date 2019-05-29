<template>
  <nav>
    <div class="container flex items-center justify-between">
      <div>
        <router-link to="/" class="logo">Stock Trader</router-link>
      </div>

      <ul class="flex items-center">
        <router-link to="/portfolio" activeClass="active" tag="li">
          <a>Portfolio</a>
        </router-link>
        <router-link to="/stocks" activeClass="active" tag="li">
          <a>Stocks</a>
        </router-link>
        <li>
          <button @click.prevent="endDay">End Day</button>
        </li>
        <li>
          <button @click.prevent="saveData">Save</button>
        </li>
        <li>
          <button @click.prevent="loadData">Load</button>
        </li>
        <li>
          <strong
            class="navbar-text navbar-right text-yellow-900 bg-yellow-300 p-2 rounded"
          >Cash: {{ funds | currency }}</strong>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
export default {
  data() {
    return {
      isDropdownOpen: false
    };
  },
  computed: {
    ...mapGetters(["stocks", "portfolio", "funds"])
  },
  methods: {
    ...mapActions({
      randomizeStocks: "randomizeStocks",
      loadDataAction: "loadData"
    }),
    endDay() {
      this.randomizeStocks();
      this.$notify({
        group: "foo",
        title: "End of the day ☀️"
      });
    },
    saveData() {
      const data = {
        funds: this.funds,
        stocks: this.stocks,
        portfolio: this.portfolio
      };
      localStorage.setItem("data", JSON.stringify(data));

      this.$notify({
        group: "foo",
        title: "Congratulations 👏🏻",
        text: "Data succesful saved",
        type: "success"
      });
    },
    loadData() {
      this.loadDataAction();
      this.$notify({
        group: "foo",
        title: "Congratulations 👏🏻",
        text: "Data succesful loaded",
        type: "success"
      });
    }
  }
};
</script>

<style lang="postcss" scoped>
nav {
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.04);
  @apply border-t-4 border-yellow-700 py-4 bg-white;
}

.logo {
  @apply font-bold;
}

ul {
  @apply list-none;
}

li {
  @apply mx-2 text-gray-800 text-sm;
}
</style>
