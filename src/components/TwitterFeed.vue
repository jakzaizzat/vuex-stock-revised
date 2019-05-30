<template>
  <div v-if="tweets.length > 0" class="twitters">
    <div class="twitter" v-for="tweet in tweets" :key="tweet.username">
      <div class="twitter__photo"></div>
      <div class="twitter__content">
        <p class="twitter__username">@jakzaizzat</p>
        <p
          class="twitter__tweet"
        >RT @PostGradProblem: In preparation for the NFL lockout, I will be spending twice as much time analyzing my fantasy baseball team during ...</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    stock: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      tweets: []
    };
  },
  methods: {
    fetchTweets() {
      axios
        .get("https://gentle-earth-27684.herokuapp.com", {
          params: {
            name: "$" + this.stock
          }
        })
        .then(res => {
          this.tweets = res;
          console.log(thos.tweets);
        });
    }
  },
  created() {
    this.fetchTweets();
  }
};
</script>



<style lang="postcss" scoped>
.twitter {
  @apply flex items-center justify-center border-b border-gray-400 py-4;
}

.twitter:last-child {
  @apply border-none;
}

.twitter__photo {
  @apply h-10 w-10 bg-gray-500 rounded-full;
}

.twitter__content {
  @apply flex-1 pl-3;
}

p {
  @apply mb-0;
}

.twitter__username {
  @apply text-gray-600 text-xs;
}
</style>