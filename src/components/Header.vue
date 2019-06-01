<template>
  <nav>
    <div class="container flex items-center justify-between">
      <div>
        <router-link to="/" class="logo">Stock Trader</router-link>
      </div>

      <ul :class="{ 'hidden': !menuShown , 'flex': menuShown }" class="sm:flex items-center">
        <router-link @click.native="openMenu" to="/portfolio" activeClass="active" tag="li">
          <a>Portfolio</a>
        </router-link>
        <router-link @click.native="openMenu" to="/stocks" activeClass="active" tag="li">
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
            class="navbar-text navbar-right text-indigo-900 bg-indigo-200 p-2 rounded"
          >Cash: {{ funds | currency }}</strong>
        </li>
      </ul>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        class="block sm:hidden icon-menu h-5 w-5 fill-current text-indigo-700 cursor-pointer"
        @click.prevent="openMenu"
      >
        <path
          class="secondary"
          fill-rule="evenodd"
          d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
        ></path>
      </svg>
    </div>
  </nav>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
export default {
  data() {
    return {
      isDropdownOpen: false,
      menuShown: false
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
    },
    openMenu() {
      this.menuShown = !this.menuShown;
    }
  }
};
</script>

<style scoped>
nav {
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.04);
  border-top-width: 4px;
  border-color: #4c51bf;
  padding-top: 1rem;
  padding-bottom: 1rem;
  background-color: #fff;
}

.logo {
  font-weight: 700;
}

ul {
  list-style-type: none;
}

li,
li button {
  margin-left: 0.5rem;
  margin-right: 0.5rem;
  color: #718096;
  font-size: 0.875rem;
  font-weight: 500;
}

li.active {
  color: #434190;
}
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@media (max-width: 640px) {
  ul {
    top: 3.725rem;
    -webkit-animation: fadeIn 0.3s ease-out both;
    animation: fadeIn 0.3s ease-out both;
    position: absolute;
    left: 0;
    flex-direction: column;
    background-color: #ebf4ff;
    width: 100%;
    z-index: 10;
    padding-top: 0.75rem;
    padding-bottom: 0.75rem;
    box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  }
  li {
    margin-top: 0.75rem;
    margin-bottom: 0.75rem;
  }
}
</style>
