<script setup lang="ts">
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFilters from "./components/AppFilters.vue";
import AppFooter, { type Stats } from "./components/AppFooter.vue";
import AppHeader from "./components/AppHeader.vue";
import AppTodoList from "./components/AppTodoList.vue";
import { computed, ref, type Ref } from "vue";
import type { Filter, Todo } from "./types";

const activeFilter: Ref<Filter> = ref("All");

const todos: Ref<Todo[]> = ref([
  { id: 0, text: "Learn the basics of Vue", completed: true },
  { id: 1, text: "Learn the basics of TypeScript", completed: false },
  { id: 2, text: "Learn the basics of Nuxt", completed: false },
]);

const addTodo = (todo: Todo): void => {
  todos.value.push(todo);
  activeFilter.value = "All";
};

const toggleTodo = (todoId: number) => {
  const curTodo = todos.value.find((todo: Todo) => todo.id === todoId);

  if (curTodo) {
    curTodo.completed = !curTodo.completed;
  }
};

const removeTodo = (todoId: number) => {
  todos.value = todos.value.filter((todo: Todo) => todo.id !== todoId);
};

const setFilter = (filter: Filter) => {
  activeFilter.value = filter;
};

const filterTodos = computed((): Todo[] => {
  switch (activeFilter.value) {
    case "Active":
      return activeTodos.value;
    case "Done":
      return doneTodos.value;
    case "All":
    default:
      return todos.value;
  }
});

const stats = computed((): Stats => {
  return { active: activeTodos.value.length, done: doneTodos.value.length };
});

const activeTodos = computed((): Todo[] => {
  return todos.value.filter((todo) => todo.completed === false);
});

const doneTodos = computed((): Todo[] => {
  return todos.value.filter((todo) => todo.completed === true);
});
</script>

<template>
  <app-header></app-header>

  <app-filters :activeFilter="activeFilter" @setFilter="setFilter"></app-filters>

  <main class="app-main">
    <app-todo-list :todos="filterTodos" @toggleTodo="toggleTodo" @removeTodo="removeTodo"></app-todo-list>

    <app-add-todo @addTodo="addTodo"></app-add-todo>
  </main>

  <app-footer :stats="stats"></app-footer>
</template>

<style scoped></style>
