<script setup lang="ts">
import type { Todo } from "@/types";
import AppTodoItem from "./AppTodoItem.vue";
import type { PropType } from "vue";

const props = defineProps({
  todos: {
    type: Array as PropType<Todo[]>,
  },
});

const emit = defineEmits<{
  toggleTodo: [id: number];
  removeTodo: [id: number];
}>();

const toggleTodo = (id: number): void => {
  emit("toggleTodo", id);
};

const removeTodo = (id: number): void => {
  emit("removeTodo", id);
};
</script>

<template>
  <ul class="todo-list">
    <app-todo-item v-for="todo in todos" :key="todo.id" :todo="todo" @toggleTodo="toggleTodo" @removeTodo="removeTodo"> </app-todo-item>
  </ul>
</template>
