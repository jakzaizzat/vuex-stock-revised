<template>
  <div class="bg-orange-800">
    <div class="home container">
      <h1>Stock Trading Demo Vuex App</h1>
      <h5>You may Save & Load your data</h5>
      <h5>Click 'End Day' to simulate the closing price</h5>
      <hr>
      <p>
        Your cash:
        <span class="cash">{{ funds | currency }}</span>
      </p>
    </div>
  </div>
</template>
<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    }
  }
};
</script>

<style lang="postcss" scoped>
.home {
  @apply py-16;
}

h1 {
  @apply text-3xl font-bold text-white;
}
h5 {
  @apply text-gray-100 text-lg leading-normal;
}
p {
  @apply text-white mt-4;
}
.cash {
  @apply font-semibold text-2xl;
}
</style>
