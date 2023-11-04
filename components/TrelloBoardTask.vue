<template>
  <div :title="task.createdAt.toLocaleString()"
    class="bg-white p-2 mb-2 rounded shadow-sm max-w-[250px] flex items-center">
    <DragHandle class="mr-2" />
    <span>{{ task.title }}</span>
  </div>
</template>

<script setup lang="ts">
import type { Task } from "~/types";

defineProps<{ task: Task }>();
</script>
