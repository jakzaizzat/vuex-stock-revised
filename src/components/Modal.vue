<template>
  <div class="modal" v-if="value">
    <div class="container">
      <div class="flex items-center justify-between py-2">
        <div class="modal__title">{{ title }}</div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          class="icon-close"
          @click.prevent="close"
        >
          <path
            class="secondary"
            fill-rule="evenodd"
            d="M15.78 14.36a1 1 0 0 1-1.42 1.42l-2.82-2.83-2.83 2.83a1 1 0 1 1-1.42-1.42l2.83-2.82L7.3 8.7a1 1 0 0 1 1.42-1.42l2.83 2.83 2.82-2.83a1 1 0 0 1 1.42 1.42l-2.83 2.83 2.83 2.82z"
          ></path>
        </svg>
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
import TwitterFeed from "../components/TwitterFeed.vue";

export default {
  props: {
    title: {
      required: true,
      type: String
    },
    value: {
      required: true
    }
  },
  components: {
    TwitterFeed
  },
  methods: {
    close() {
      this.$emit("input", !this.value);
    }
  }
};
</script>


<style lang="postcss">
.modal {
  background-color: rgba(0, 0, 0, 0.7);
  @apply absolute top-0 left-0 min-h-screen w-full flex items-center justify-center z-20;
}

.modal .container {
  @apply bg-white p-4 max-w-sm rounded border border-gray-200 text-left shadow my-4;
}

.modal__title {
  @apply font-semibold capitalize;
}

.modal svg {
  @apply h-6 w-6  cursor-pointer fill-current text-gray-500;
}

.modal svg:hover {
  @apply text-black;
}

.modal p {
  @apply mb-3 text-sm text-gray-800;
}

.modal input {
  @apply appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight;
}
.modal input:focus {
  @apply outline-none bg-white border-gray-500;
}

.modal .btn {
  @apply border-none flex items-center justify-center;
}

.modal .btn img {
  @apply h-6 w-auto mr-2;
}
</style>
