<template>
  <div class="w-full md:w-1/2 px-2 mb-4">
    <div class="card">
      <div class="title">
        {{ stock.name }}
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          width="24"
          height="24"
        >
          <path
            class="heroicon-ui"
            d="M12 2a10 10 0 1 1 0 20 10 10 0 0 1 0-20zm0 2a8 8 0 1 0 0 16 8 8 0 0 0 0-16zm0 9a1 1 0 0 1-1-1V8a1 1 0 0 1 2 0v4a1 1 0 0 1-1 1zm0 4a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"
          ></path>
        </svg>
      </div>
      <div class="body">
        <div class="price">{{stock.price | currency}}</div>
        <p>Lorem Ipsum Lorem Ipsum</p>

        <input type="number" placeholder="Quantity" v-model="quantity">

        <button class="btn" @click="buyStock" :disabled="insufficientFunds || quantity<=0">Buy</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    stock: {
      type: Object,
      required: true
    },
    type: {
      type: String
    }
  },
  data() {
    return {
      quantity: 0
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds;
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.$store.dispatch("buyStock", order);
      this.quantity = 0;
    }
  }
};
</script>

<style lang="postcss" scoped>
.card {
  @apply border-2 border-gray-400 rounded bg-white text-center;
}
.title {
  @apply font-semibold text-gray-700 py-3 border-b border-gray-400 relative;
}
svg {
  top: 10px;
  right: 10px;
  @apply h-4 w-4 fill-current text-gray-800 absolute opacity-75 cursor-pointer;
}
.body {
  @apply p-4;
}
.price {
  @apply text-4xl;
}
p {
  @apply text-sm text-gray-600 mb-4;
}

input {
  @apply bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight mb-4;
}
</style>