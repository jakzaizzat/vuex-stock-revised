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
  position: absolute;
  top: 0;
  left: 0;
  min-height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 20;
}

.modal .container {
  background-color: #fff;
  padding: 1rem;
  max-width: 24rem;
  border-radius: 0.25rem;
  border-width: 1px;
  border-color: #edf2f7;
  text-align: left;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  margin-top: 1rem;
  margin-bottom: 1rem;
}

.modal__title {
  font-weight: 600;
  text-transform: capitalize;
}

.modal svg {
  height: 1.5rem;
  width: 1.5rem;
  cursor: pointer;
  fill: currentColor;
  color: #a0aec0;
}

.modal svg:hover {
  color: #000;
}

.modal p {
  margin-bottom: 0.75rem;
  font-size: 0.875rem;
  color: #2d3748;
}

.modal input {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  display: block;
  width: 100%;
  background-color: #edf2f7;
  color: #4a5568;
  border-width: 1px;
  border-color: #edf2f7;
  border-radius: 0.25rem;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  padding-left: 1rem;
  padding-right: 1rem;
  line-height: 1.25;
}
.modal input:focus {
  outline: 0;
  background-color: #fff;
  border-color: #a0aec0;
}

.modal .btn {
  border-style: none;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* .modal .btn img {
  @apply h-6 w-auto mr-2;
} */
</style>
