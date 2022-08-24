<script setup lang="ts">
import { ref } from 'vue';

// give each todo a unique id
let id = 0;

type Todo = {
  id: typeof id,
  text: string
};

const createTodo = (text: Todo['text']): Todo => {
  const todo: Todo = {
    id,
    text,
  };
  id += 1;
  return todo;
};

const newTodo = ref('');
const todos = ref<Todo[]>([
  createTodo('Learn HTML'),
  createTodo('Learn JavaScript'),
  createTodo('Learn Vue'),
]);

const addTodo = () => {
  todos.value.push(createTodo(newTodo.value));
  newTodo.value = '';
};

const removeTodo = (todo: Todo) => {
  const index = todos.value.indexOf(todo);

  if (Number.isInteger(index) && index >= 0) {
    todos.value.splice(index, 1);
  }
};
</script>

<template>
  <form @submit.prevent="addTodo">
    <label for="input-todo-text">Type To-Do
      <input
        id="input-todo-text"
        v-model="newTodo"
        type="text"
      >
    </label>
    <button
      type="submit"
      role="button"
    >
      Add Todo
    </button>
  </form>
  <ul>
    <li
      v-for="todo in todos"
      :key="todo.id"
    >
      {{ todo.text }}
      <button @click="removeTodo(todo)">
        ❌
      </button>
    </li>
  </ul>
</template>
