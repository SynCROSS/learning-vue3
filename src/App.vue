<script setup lang="ts">
import { computed, ref } from 'vue';

// give each todo a unique id
let id = 0;

type Todo = {
  id: typeof id,
  text: string,
  done: boolean,
};

/**
 * Create a new Todo Object By Text
 * @param {Todo['text']} text Todo's Text
 * @return {Todo} new Todo Object
 */
const createTodo = (text: Todo['text'], done = false): Todo => {
  const todo: Todo = {
    id,
    text,
    done,
  };
  id += 1;
  return todo;
};

const newTodo = ref<Todo['text']>('');
const hideCompleted = ref<Todo['done']>(false);
const todos = ref<Todo[]>([
  createTodo('Learn HTML', true),
  createTodo('Learn JavaScript', true),
  createTodo('Learn Vue'),
]);

/**
 * Add a new Todo Object To the list of Todo
 */
const addTodo = () => {
  todos.value.push(createTodo(newTodo.value));
};

/**
 * Reset Input Value
 */
const resetNewTodo = () => {
  newTodo.value = '';
};

/**
 * Submit Event Handler Of Form
 */
const onSubmit = () => {
  addTodo();
  resetNewTodo();
};

const removeTodo = (todo: Todo) => {
  const index = todos.value.indexOf(todo);

  if (Number.isInteger(index) && index >= 0) {
    todos.value.splice(index, 1);
  }
};

const toggleHidingTodo = () => {
  hideCompleted.value = !hideCompleted.value;
};

const filteredTodos = computed(() => {
  // return filtered todos based on
  // `todos.value` & `hideCompleted.value`
  if (hideCompleted.value) {
    return todos.value.filter(todo => !todo.done);
  }
  return todos.value;
});

</script>

<template>
  <form @submit.prevent="onSubmit">
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
      v-for="todo in filteredTodos"
      :key="todo.id"
    >
      <input
        v-model="todo.done"
        type="checkbox"
      >
      <span :class="{ done: todo.done }">
        {{ todo.text }}
      </span>
      <button @click="removeTodo(todo)">
        ❌
      </button>
    </li>
  </ul>
  <button @click="toggleHidingTodo">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
