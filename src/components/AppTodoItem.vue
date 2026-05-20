<script setup lang="ts">
import type { PropType } from "vue";
import type { Todo } from "@/types";

const props = defineProps({
  todo: {
    type: Object as PropType<Todo>,
    required: true,
  },
});

const emit = defineEmits<{
  toggleTodo: [id: number];
  removeTodo: [id: number];
}>();
</script>

<template>
  <li class="todo-item" :class="{ 'todo-item--done': props.todo.completed }" @click="$emit('toggleTodo', props.todo.id)">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ props.todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="$emit('removeTodo', props.todo.id)">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>
