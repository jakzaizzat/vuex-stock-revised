<template>
  <div>
    <drop
      class="drag"
      @drop="handleDrop"
      :class="{ active }"
      @dragover="active = true"
      @dragleave="active = false"
    >
      <span>Drag stock over here</span>
    </drop>

    <Modal :title="selectedStock.name || '' " v-model="stockModal">
      <p>
        How many unit of
        <span class="font-semibold">{{ selectedStock.name }}</span>
        do you want to {{ typeTransaction }}?
      </p>
      <input type="number" placeholder="Quantity" v-model="quantity">
      <button class="btn capitalize" @click="submit" :disabled="isDisabled">{{ typeTransaction }}</button>
    </Modal>
  </div>
</template>

<script>
import Modal from "../components/Modal.vue";
import { mapActions } from "vuex";
export default {
  components: {
    Modal
  },
  props: {
    type: {
      required: true,
      type: String
    }
  },
  data() {
    return {
      active: false,
      stockModal: false,
      selectedStock: "",
      quantity: 0
    };
  },
  methods: {
    handleDrop(data, event) {
      this.active = false;
      this.selectedStock = data.stock;
      this.stockModal = true;
    },
    submit() {
      if (this.type === "portfolio") {
        this.buyStock();
      }
      if (this.type === "stock") {
        this.sellStock();
      }
      this.selectedStock = "";
      this.stockModal = false;

      this.$notify({
        group: "foo",
        title: "Congratulations 👏🏻",
        text: "Successful transaction",
        type: "success"
      });
    },
    buyStock() {
      const order = {
        stockId: this.selectedStock.id,
        stockPrice: this.selectedStock.price,
        quantity: parseInt(this.quantity)
      };
      this.$store.dispatch("buyStock", order);
    },
    ...mapActions({ sellStockAction: "sellStock" }),
    sellStock() {
      const order = {
        stockId: this.selectedStock.id,
        stockPrice: this.selectedStock.price,
        quantity: this.quantity
      };
      this.sellStockAction(order);
    }
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    typeTransaction() {
      if (this.type == "portfolio") {
        return "buy";
      } else {
        return "sell";
      }
    },
    insufficientFunds() {
      return this.quantity * this.selectedStock.price > this.funds;
    },
    isDisabled() {
      var status = false;
      if (
        this.type === "portfolio" &&
        this.quantity * this.selectedStock.price > this.funds
      ) {
        status = true;
      }

      if (
        this.type === "stock" &&
        this.quantity > this.selectedStock.quantity
      ) {
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

<style lang="postcss" scoped>
.drag {
  @apply bg-gray-700 h-32 w-auto rounded shadow-inner flex items-center justify-center;
}

.drag.active {
  @apply bg-black;
}

.drag span {
  @apply text-gray-400;
}
</style>
