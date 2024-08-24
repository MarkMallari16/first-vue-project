<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
import { reactive, ref } from "vue";

const count = ref(0);
const message = ref("Hello Vue");
const text = ref("First Text");
const checked = ref(false);
const studentType = ref(null);
const checkCourses = ref([]);

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

    <p>{{ text }}</p>

    <div>Checked Names: {{ checkCourses }}</div>
    <div>
      <input type="checkbox" id="bsit" value="BSIT" v-model="checkCourses" />
      <label for="bsit">BSIT</label>

      <input type="checkbox" id="bscs" value="BSCS" v-model="checkCourses" />
      <label for="bscs">BSCS</label>

      <input type="checkbox" id="bsce" value="BSCE" v-model="checkCourses" />
      <label for="bsce">BSCE</label>

      <div>Student Type: {{ studentType }}</div>

      <input type="radio" id="regular" value="Regular" v-model="studentType" />
      <label for="regular">Regular</label>

      <input type="radio" id="irregular" value="Irregular" v-model="studentType" />
      <label for="irregular">Irregular</label>
    </div>
  </div>
</template>

<style scoped></style>
