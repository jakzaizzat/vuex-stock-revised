<template>
  <div>
    <div v-if="tweets.length > 0" class="twitters">
      <div class="twitter" v-for="tweet in tweets" :key="tweet.username">
        <img :src="tweet.profile" class="twitter__photo">
        <div class="twitter__content">
          <a
            :href=" 'https://twitter.com/' + tweet.username "
            class="twitter__username"
            target="_blank"
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



<style  scoped>
.twitter {
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom-width: 1px;
  border-color: #cbd5e0;
  padding-top: 1rem;
  padding-bottom: 1rem;
}

.twitter:last-child {
  border-style: none;
}

.twitter__photo {
  height: 2.5rem;
  width: 2.5rem;
  background-color: #a0aec0;
  border-radius: 9999px;
}

.twitter__content {
  flex: 1 1 0%;
  padding-left: 0.75rem;
}

p {
  margin-bottom: 0;
}

.twitter__username {
  color: #718096;
  font-size: 0.75rem;
}

.twitter__username:hover {
  color: #4299e1;
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