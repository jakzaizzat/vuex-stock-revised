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

<style lang="postcss" scoped>
nav {
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.04);
  @apply border-t-4 border-indigo-700 py-4 bg-white;
}

.logo {
  @apply font-bold;
}

ul {
  @apply list-none;
}

li,
li button {
  @apply mx-2 text-gray-600 text-sm font-medium;
}

li.active {
  @apply text-indigo-800;
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
    animation: fadeIn 0.3s ease-out both;
    @apply absolute left-0 flex-col bg-indigo-100 w-full z-10 py-3 shadow;
  }
  li {
    @apply my-3;
  }
}
</style>
