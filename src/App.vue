<script setup>
import { ref } from "vue";

const count = ref(0);
let id = 0;
const newTodo = ref("");
const todos = ref([
  { id: id++, text: "Kain", done: true },
  { id: id++, text: "Tulog", done: false },
]);

const editingTodoId = ref(null);
const editingTodoText = ref("");

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
function addTodo() {
  if (newTodo.value.trim() === "") {
    alert("Please enter a task");
    return;
  }
  todos.value.push({ id: id++, text: newTodo.value });
  newTodo.value = "";
}

function removeTodo(id) {
  todos.value = todos.value.filter((todo) => todo.id != id);
}
function editTodo(id) {
  const todo = todos.value.find((todo) => todo.id === id);

  if (todo) {
    editingTodoId.value = id;
    editingTodoText.value = todo.text;
  }
}
function saveTodo() {
  const todo = todos.value.find((todo) => todo.id === editingTodoId.value);

  if (todo) {
    todo.text = editingTodoText.value;
    editingTodoId.value = null;
    editingTodoText.value = "";
  }
}
</script>

<template>
  <div>
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

    <div class="m-20">
      <h1 class="text-4xl text-center mt-20">Simple To-do List</h1>
      <h2 class="text-2xl mb-5">Tasks: {{ todos.length }}</h2>

      <form @submit.prevent="addTodo" class="mb-5 flex gap-5">
        <input
          v-model="newTodo"
          class="input input-bordered w-1/2"
          placeholder="add task here"
        />
        <button type="submit" class="btn btn-primary">Add</button>
      </form>
      <div>
        <div
          class="mb-2 flex items-center justify-between w-1/2"
          v-for="todo in todos"
          :key="todo.id"
        >
          <input type="checkbox" v-model="todo.done" class="checkbox"/>

          <div v-if="editingTodoId === todo.id" class="flex gap-2">
            <input
              v-model="editingTodoText"
              class="input input-bordered"
              placeholder="Edit task here"
            />
            <button @click="saveTodo" class="btn btn-primary">Save</button>
          </div>
          <p v-else class="font-medium" :class="{'line-through': todo.done, 'text-green-500': todo.done }">{{ todo.text }}</p>
          <div class="flex gap-2">
            <button @click="editTodo(todo.id)" class="btn btn-secondary">Edit</button>
            <button @click="removeTodo(todo.id)" class="btn btn-error">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.text {
  color: blue;
}
</style>
