<script setup>
import { ref, computed } from "vue";

let id = 0;

const newTodo = ref("");

const todos = ref([
  { id: id++, text: "Kain", done: true },
  { id: id++, text: "Tulog", done: false },
]);

const editingTodoId = ref(null);
const editingTodoText = ref("");
const hideCompleted = ref(false);

const sortedOrder = ref("asc");
const hasError = ref(false);
const characterCount = computed(() => {
  return newTodo.value.length;
});


function addTodo() {
  if (newTodo.value.trim() === "") {
    hasError.value = true;
    return;
  }
  todos.value.push({ id: id++, text: newTodo.value });
  newTodo.value = "";
  hasError.value = false;
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

function hide() {
  hideCompleted.value = !hideCompleted.value;
}

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? [...todos.value].filter((todo) => !todo.done)
    : todos.value;
});

const sortedTodos = computed(() => {
  const sortedArray = filteredTodos.value.sort((a, b) => {
    if (sortedOrder.value === "asc") {
      return a.text.localeCompare(b.text);
    } else {
      return b.text.localeCompare(a.text);
    }
  });
  return sortedArray;
});
</script>

<template>
  <div class="m-20">
    <h1 class="text-4xl text-center mt-20">Simple To-do List</h1>
    <div class="mt-10 mb-5 flex items-center w-1/2 justify-between">
      <h2 class="text-2xl">Number of Tasks: {{ todos.length }}</h2>
      <select v-model="sortedOrder" className="select w-full max-w-xs">
        <option disabled selected>Sort task</option>
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
        <option value="reverse">Reverse</option>
        <option value="">Normal</option>
      </select>
    </div>

    <form @submit.prevent="addTodo" class="mb-2 flex gap-5">
      <input
        v-model="newTodo"
        class="input input-bordered w-1/2"
        placeholder="Enter Task"
        maxlength="50"
      />
      <button type="submit" class="btn btn-primary">Add</button>
    </form>
    <div class="mb-5">
      <p class="mb-1" v-if="hasError" :class="{ 'text-red-500': hasError }">
        You must enter a task!
      </p>
      <p>{{ characterCount }}/50</p>
    </div>
    <div>
      <div class="w-1/2 text-center font-medium" v-if="todos.length == 0">
        No Task Today
      </div>
      <div
        v-else
        class="mb-2 flex items-center justify-between w-1/2"
        v-for="todo in sortedTodos"
        :key="todo.id"
      >
        <input type="checkbox" v-model="todo.done" class="checkbox" />

        <div v-if="editingTodoId === todo.id" class="flex gap-2">
          <input
            v-model="editingTodoText"
            class="input input-bordered"
            placeholder="Edit task here"
          />
        </div>
        <p
          v-else
          class="font-medium"
          :class="{ 'line-through': todo.done, 'text-green-500': todo.done }"
        >
          {{ todo.text }}
        </p>
        <div class="flex gap-2">
          <button
            v-if="editingTodoId !== todo.id"
            @click="editTodo(todo.id)"
            class="btn btn-secondary"
          >
            Edit
          </button>
          <button v-else @click="saveTodo" class="btn btn-primary">Save</button>
          <button @click="removeTodo(todo.id)" class="btn btn-error">Delete</button>
        </div>
      </div>
      <div v-if="todos.length > 0">
        <button @click="hide" class="btn btn-ghost">
          {{ hideCompleted ? "Show All" : "Hide Completed" }}
        </button>
      </div>
    </div>
  </div>
</template>
