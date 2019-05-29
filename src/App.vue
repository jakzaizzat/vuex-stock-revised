<template>
  <div class="h-full">
    <AppHeader></AppHeader>
    <transition name="slide" mode="out-in">
      <router-view></router-view>
    </transition>
    <notifications group="foo"/>
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
  @apply min-h-screen;
}
.container {
  @apply max-w-4xl mx-auto px-2;
}

.btn {
  @apply bg-gray-800 text-white px-6 py-1 rounded font-semibold flex items-center justify-center;
}

.btn:disabled {
  @apply bg-gray-400;
}

.btn:hover {
  @apply text-gray-800 bg-white;
}

.btn-outline {
  @apply text-gray-800 border border-gray-500 bg-white;
}

.btn svg {
  @apply h-4 w-4 mr-2 fill-current text-gray-500;
}

input {
  @apply bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight mb-4;
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
