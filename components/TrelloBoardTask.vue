<template>
  <div class="focus:outline-none focus:bg-gray-300 bg-white p-2 mb-2 rounded shadow-sm max-w-[250px] flex items-center"
    @focus="focused = true" @blur="focused = false" :title="task.createdAt.toLocaleString()" tabindex="0">
    <DragHandle class="mr-2" />
    <span>{{ task.title }}</span>
  </div>
</template>

<script setup lang="ts">
import type { Task } from "~/types";

const props = defineProps<{ task: Task }>();
const emit = defineEmits<{ (e: "delete", payload: string): void }>();

const focused = ref(false);

onKeyStroke("Backspace", () => {
  if (focused.value) {
    emit("delete", props.task.id);
  }
});
</script>
