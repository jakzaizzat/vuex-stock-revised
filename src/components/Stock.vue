<template>
  <div class="w-full md:w-1/2 px-2 mb-4">
    <div class="stock">
      <div class="title">
        <drag :transfer-data="{ stock }" drop-effect="move" class="cursor-move">{{ stock.name }}</drag>
        <svg
          @click="openModal = true"
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
        <p
          v-if="stock.quantity"
        >{{ stock.quantity }} units - {{ stock.quantity * stock.price | currency }}</p>

        <input type="number" placeholder="Quantity" v-model="quantity">

        <button class="btn" @click="submit" :disabled="isDisabled">
          <span class="capitalize">{{ this.types }}</span>
        </button>

        <Modal title="Recent 5 tweets" v-model="openModal">
          <TwitterFeed :stock="stock.name" :fetch="openModal"/>
        </Modal>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import Modal from "../components/Modal.vue";
import TwitterFeed from "../components/TwitterFeed.vue";

export default {
  props: {
    stock: {
      type: Object,
      required: true
    },
    types: {
      type: String
    }
  },
  components: {
    Modal,
    TwitterFeed
  },
  data() {
    return {
      quantity: 0,
      openModal: false
    };
  },
  methods: {
    submit() {
      if (this.types === "buy") {
        this.buyStock();
      }
      if (this.types === "sell") {
        this.sellStock();
      }
      this.quantity = 0;
      this.$notify({
        group: "foo",
        title: "Congratulations 👏🏻",
        text: "Successful transaction",
        type: "success"
      });
    },
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: parseInt(this.quantity)
      };
      this.$store.dispatch("buyStock", order);
    },
    ...mapActions({ sellStockAction: "sellStock" }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.sellStockAction(order);
    }
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds;
    },
    isDisabled() {
      var status = false;
      if (
        this.types === "buy" &&
        this.quantity * this.stock.price > this.funds
      ) {
        status = true;
      }

      if (this.types === "sell" && this.quantity > this.stock.quantity) {
        status = true;
      }

      if (this.quantity <= 0) {
        status = true;
      }

      return status;
    }
  }
};
</script>

<style  scoped>
.stock {
  border-width: 2px;
  border-color: #cbd5e0;
  border-radius: 0.25rem;
  background-color: #fff;
  text-align: center;
}
.title {
  font-weight: 600;
  color: #4a5568;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  border-bottom-width: 1px;
  border-color: #cbd5e0;
  position: relative;
}
svg {
  top: 10px;
  right: 10px;
  height: 1rem;
  width: 1rem;
  fill: currentColor;
  color: #2d3748;
  position: absolute;
  opacity: 0.75;
  cursor: pointer;
}
.body {
  padding: 1rem;
}
.price {
  font-size: 2.25rem;
  margin-bottom: 0.5rem;
}
p {
  font-size: 0.875rem;
  color: #718096;
  margin-bottom: 1rem;
}
</style>
