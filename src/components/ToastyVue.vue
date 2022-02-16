<template>
  <div class="toast-container">
    <TransitionGroup name="toastlist" tag="div">
      <div v-for="toast in toasts" :key="toast.id" class="toast">
        <slot></slot>
        <div class="wrapper">
          <div class="title">{{ toast.title.toUpperCase() }}</div>
          <div class="content">{{ toast.content }}</div>
        </div>
        <button class="close" @click="this.$emit('clear-one', toast.id)">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        </button>
      </div>
    </TransitionGroup>
  </div>
</template>

<script setup>
import { watchEffect } from "vue";
const emit = defineEmits(["clear-one"]);
const props = defineProps({
  toasts: {
    type: Array,
    default: () => [
      {
        title: {
          type: String,
        },
        content: {
          type: String,
        },
      },
    ],
  },
});
watchEffect(() => {
  if (props.toasts.length > 0) {
    const addedItemId = props.toasts[0].id;
    setTimeout(() => {
      emit("clear-one", addedItemId);
    }, 5000);
  }
});
</script>

<style>
.toast-container {
  width: 22em;
  position: absolute;
  top: 0.75em;
  right: 0.75em;
  z-index: 10;
}
.toast {
  background-color: #ffffff;
  border-radius: 5px;
  text-align: left;
  display: flex;
  align-items: stretch;
  overflow: hidden;
  justify-content: space-between;
  margin-bottom: 10px;
  box-shadow: 0 8px 17px rgba(0, 0, 0, 0.2);
  -webkit-box-shadow: 0 8px 17px rgba(0, 0, 0, 0.2);
  -moz-box-shadow: 0 8px 17px rgba(0, 0, 0, 0.2);
}
.icon {
  width: 3em;
  display: flex;
  background-color: #d78407;
  align-items: center;
  justify-content: center;
}
.icon > svg {
  stroke: #ffffff;
  width: 1.5em;
  height: 1.5em;
}
button.close {
  background-color: transparent;
  align-self: flex-start;
  padding: 0.5em;
}
button.close > svg {
  stroke: #666666;
  width: 1.5em;
  height: 1.5em;
}
.title {
  font-weight: bold;
  font-size: 1.2em;
  padding: 0.5em 0.75em 0.25em 0.75em;
}
.content {
  padding: 0.5em 0.75em;
}
.wrapper {
  padding: 0.5em;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}
.toastlist-enter-from {
  opacity: 50%;
  transform: translateX(22em);
}
.toastlist-enter-active {
  transition: all 0.3s cubic-bezier(0.5, 1.5, 1, 1);
}
.toastlist-leave-active {
  transition: all 0.3s cubic-bezier(0.88, -0.33, 1, 1);
}
.toastlist-leave-to {
  opacity: 0;
  transform: translateX(22em);
}
</style>
