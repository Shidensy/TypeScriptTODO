<script setup lang="ts">
import type { Filter } from "@/types";
import type { PropType } from "vue";

const filters: Filter[] = ["Active", "All", "Done"];

const props = defineProps({
  activeFilter: {
    type: String as PropType<Filter>,
    required: true,
  },
});

const emits = defineEmits<{
  setFilter: [filter: Filter];
}>();
</script>

<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button class="button" :class="{ 'button--primary': activeFilter === filter }" v-for="filter in filters" :key="filter" @click="$emit('setFilter', filter)">
        {{ filter }}
      </button>
    </section>
  </aside>
</template>
