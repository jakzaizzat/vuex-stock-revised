<template>
  <div>
    <div v-if="tweets.length > 0" class="twitters">
      <div class="twitter" v-for="tweet in tweets" :key="tweet.username">
        <img :src="tweet.profile" class="twitter__photo">
        <div class="twitter__content">
          <a
            :href=" 'https://twitter.com/' + tweet.username "
            class="twitter__username"
          >@{{ tweet.username }}</a>
          <p class="twitter__tweet">{{ tweet.message }}</p>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="lds-dual-ring"></div>
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
          this.tweets = res.data;
          console.log(this.tweets);
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

.twitter__username:hover {
  @apply text-blue-500;
}

.loading {
  @apply text-center font-semibold;
}

.lds-dual-ring {
  display: block;
  width: 32px;
  height: 32px;
  margin: 20px auto 0;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 23px;
  height: 23px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #4c51bf;
  border-color: #4c51bf transparent #4c51bf transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>