<template>
  <div class="w-full md:w-1/4 sidebar" v-show="show">
    <div>
      <h2>Portfolio</h2>

      <ul>
        <li v-for="stock in stocks" :key="stock.id">{{ stock.name }} @${{stock.price | currency}}</li>
      </ul>
    </div>

    <div class="sidebar__drag"></div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  props: {
    show: {
      required: true,
      type: Boolean
    }
  },
  computed: {
    ...mapGetters({ stocks: "portfolio" })
  }
};
</script>


<style lang="postcss" scoped>
.sidebar {
  @apply bg-gray-800 p-4 flex flex-col justify-between;
}

.sidebar h2 {
  @apply text-white font-semibold mb-4 text-xl;
}

.sidebar ul {
  @apply list-inside;
}

.sidebar ul li {
  @apply text-gray-200 mb-4;
}

.sidebar__drag {
  @apply bg-gray-700 h-32 w-auto rounded shadow-inner;
}
</style>
