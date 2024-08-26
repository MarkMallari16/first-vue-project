<script setup>
import { ref } from "vue";
const count = ref(0);
function increment() {
  count.value++;
}
function decrement() {
  if (count.value > 0) {
    count.value--;
  }
}
function reset() {
  count.value = 0;
}
</script>

<template>
  <div class="flex justify-center">
    <div>
      <h1 class="text-center text-3xl my-4">Count: {{ count }}</h1>
      <div class="flex gap-3">
        <button @click="decrement" class="btn btn-error">Decrement</button>
        <button @click="reset" class="btn btn-secondary">Reset</button>
        <button @click="increment" class="btn btn-primary">Increment</button>
      </div>
    </div>
  </div>
</template>
