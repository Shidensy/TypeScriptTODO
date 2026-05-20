<script setup lang="ts">
import type { Todo } from "@/types";
import { type Ref, ref } from "vue";

const isFormVisible: Ref<boolean> = ref(false);
const inputText: Ref<string> = ref("");

const showForm = (): void => {
  isFormVisible.value = !isFormVisible.value;
};

const closeForm = (): void => {
  isFormVisible.value = false;
};

const emit = defineEmits<{
  addTodo: [todo: Todo];
}>();

const addTodo = (): void => {
  emit("addTodo", { id: Date.now(), text: inputText.value, completed: false });
  inputText.value = "";
  closeForm();
};
</script>

<template>
  <section class="add-todo">
    <form class="add-todo__form" v-if="isFormVisible" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click="closeForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="inputText" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button class="add-todo__show-form-button" v-else @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>
