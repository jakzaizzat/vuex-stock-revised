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

      <button class="btn" @click.prevent="fetch">Fetch Twitter</button>
    </div>
  </div>
</template>
<script>
import axios from "axios";

const config = {
  headers: {
    Authorization:
      'OAuth oauth_consumer_key="7AxS1yrDUk1fuGMiCPdL3kR3y", oauth_nonce="1a9dqt80RBxOpxaXooHGYw2NLO0qHhDU", oauth_signature="Sk658Qit6ZzusABwWf7iMobiMcs%3D", oauth_signature_method="HMAC-SHA1", oauth_timestamp="1559187938", oauth_token="2919810050-uY72CPRxzY0ADil6SDUSNwsbAg9Fje4xj7nvkbr", oauth_version="1.0"'
  },
  params: {
    q: "$app"
  }
};

export default {
  methods: {
    fetch() {
      console.log("dah tekan");
      // axios
      //   .get(
      //     "https://cors-anywhere.herokuapp.com/https://api.twitter.com/1.1/search/tweets.json",
      //     config
      //   )
      //   .then(res => {
      //     console.log(res);
      //   })
      //   .catch(err => {
      //     console.log(err);
      //   });
    }
  },
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
