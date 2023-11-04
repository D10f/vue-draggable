<template>
  <div>
    <textarea class="focus:bg-white focus:shadow resize-none rounded w-full border-none !outline-none p-1" v-model="title"
      @blur="focused = false" @focus="focused = true" @keydown.tab="createTask" @keydown.enter="createTask"
      :class="{ 'h-7': !focused, 'h-20 p-2': focused }"
      :placeholder="focused ? 'Enter a title for this task' : '+ Add a task'" />
  </div>
</template>

<script setup lang="ts">
import type { Task } from "~/types";
import { nanoid } from "nanoid";

const emit = defineEmits<{ (e: "add", payload: Task): void }>();
const focused = ref(false);
const title = ref("");

function createTask(e: Event) {
  if (title.value.trim() === "") return;
  e.preventDefault();

  emit("add", {
    id: nanoid(),
    title: title.value.trim(),
    createdAt: new Date(),
  });

  title.value = "";
}
</script>
