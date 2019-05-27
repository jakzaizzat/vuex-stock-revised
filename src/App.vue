<template>
  <div>
    <AppHeader></AppHeader>
    <div class="container">
      <transition name="slide" mode="out-in">
        <router-view></router-view>
      </transition>
    </div>
  </div>
</template>

<script>
import AppHeader from "./components/Header.vue";
export default {
  components: {
    AppHeader
  },
  created() {
    // Vue instance is created in the lifecycle
    this.$store.dispatch("initStocks");
  }
};
</script>

<style lang="postcss">
@import "./assets/css/tailwind.css";
body {
  background-color: #f5f7fa;
}
.container {
  @apply max-w-2xl mx-auto px-2;
}

.slide-enter-active {
  animation: slide-in 200ms ease-out forwards;
}
.slide-leave-active {
  animation: slide-out 200ms ease-out forwards;
}
@keyframes slide-in {
  from {
    transform: translateY(-30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes slide-out {
  from {
    transform: translateY(0);
    opacity: 1;
  }
  to {
    transform: translateY(-30px);
    opacity: 0;
  }
}
</style>
