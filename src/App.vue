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

<style lang="css">
@import "./assets/css/tailwind.css";
body {
  background-color: #f5f7fa;
  min-height: 100vh;
}
.container {
  max-width: 56rem;
  margin-left: auto;
  margin-right: auto;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}

.btn {
  background-color: #434190;
  color: #fff;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
  border-radius: 0.25rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn:disabled {
  background-color: #7f9cf5;
}

.btn:hover {
  color: #434190;
  background-color: #fff;
}

.btn-outline {
  color: #434190;
  border-width: 1px;
  border-color: #667eea;
  background-color: #fff;
}

.btn svg {
  height: 1rem;
  width: 1rem;
  margin-right: 0.5rem;
  fill: currentColor;
  color: #667eea;
}

input {
  background-color: #edf2f7;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border-width: 2px;
  border-color: #edf2f7;
  border-radius: 0.25rem;
  width: 100%;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  color: #4a5568;
  line-height: 1.25;
  margin-bottom: 1rem;
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
