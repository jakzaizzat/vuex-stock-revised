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
          <a href="#" @click="endDay">End Day</a>
        </li>
        <li>
          <a href="#" @click="saveData">Save</a>
        </li>
        <li>
          <a href="#" @click="loadData">Load</a>
        </li>
        <li>
          <strong
            class="navbar-text navbar-right text-yellow-900 bg-yellow-300 p-2 rounded"
          >Cash: {{ funds | currency }}</strong>
        </li>
      </ul>

      <!-- <div class="collapse navbar-collapse flex items-center justify-center">
        <ul class>
          <router-link to="/portfolio" activeClass="active" tag="li">
            <a>Portfolio</a>
          </router-link>
          <router-link to="/stocks" activeClass="active" tag="li">
            <a>Stocks</a>
          </router-link>
        </ul>
        <strong class="navbar-text navbar-right">Cash: {{ funds | currency }}</strong>
        <ul class="nav navbar-nav navbar-right">
          <li>
            <a href="#" @click="endDay">End Day</a>
          </li>
          <li
            class="dropdown"
            :class="{open: isDropdownOpen}"
            @click="isDropdownOpen = !isDropdownOpen"
          >
            <a
              href="#"
              class="dropdown-toggle"
              data-toggle="dropdown"
              role="button"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Save & Load
              <span class="caret"></span>
            </a>
            <ul class="dropdown-menu">
              <li>
                <a href="#" @click="saveData">Save</a>
              </li>
              <li>
                <a href="#" @click="loadData">Load</a>
              </li>
            </ul>
          </li>
        </ul>
      </div>-->
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
    },
    saveData() {
      const data = {
        funds: this.funds,
        stocks: this.stocks,
        portfolio: this.portfolio
      };
      localStorage.setItem("data", JSON.stringify(data));
    },
    loadData() {
      this.loadDataAction();
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
