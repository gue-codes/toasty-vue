<template>
  <section class="main">
    <h1>Toasty-Vue Demo</h1>
    <p>Just click the Button to try it out 😃</p>
  </section>
  <section>
    <button class="primary" @click="addOne">Show me the Toast!</button>
  </section>
  <ToastyVue :toasts="toasts" @clear-one="clearOne">
    <div class="icon">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
        />
      </svg>
    </div>
  </ToastyVue>
</template>

<script setup>
import { ref } from "vue";
import ToastyVue from "./components/ToastyVue.vue";
const toasts = ref([]);
function clearOne(id) {
  toasts.value = toasts.value.filter((item) => item.id !== id);
}
function addOne() {
  const fakeid = Date.now().toString();
  toasts.value.push({
    id: fakeid,
    title: "This is the Title",
    content: "This is the content",
  });
}
</script>

<style>
body {
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-family: Helvetica, Arial, sans-serif;
  background-color: #f7f7f7;
  color: #222222;
}
h1 {
  font-size: 2em;
}
button {
  cursor: pointer;
  border: none;
  border-radius: 5px;
  padding: 0.5em 1em;
}
button.primary {
  background-color: #d78407;
  color: #ffffff;
  font-size: 1.5em;
  font-weight: bold;
}
button.primary:hover {
  background-color: #e6951d;
}
</style>
