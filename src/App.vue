<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
import { reactive, ref } from "vue";

const count = ref(0);
const message = ref("Hello Vue");

function increment() {
  count.value++;
}
function decrement() {
  count.value--;
}
function reset() {
  count.value = 0;
}
</script>

<template>
  <div>
    <h1>Count: {{ count }}</h1>

    <button @click="decrement">Decrement</button>
    <button @click="reset">Reset</button>
    <button @click="increment">Increment</button>

    <h3>{{ message }}</h3>
  </div>
</template>

<style scoped>


</style>
