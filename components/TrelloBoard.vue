<template>
  <div>
    <draggable :list="columns" :animation="150" item-key="id" group="columns" handle=".drag-handle"
      class="flex gap-4 overflow-x-auto items-start">
      <div v-for="column in columns" :key="column.id" class="column bg-gray-200 p-5 rounded min-w-[250px]">
        <header>
          <DragHandle />
          <h3 class="font-bold mb-4">{{ column.title }}</h3>
        </header>

        <draggable :list="column.tasks" :animation="150" item-key="id"
          :group="{ name: 'tasks', pull: ctrl ? 'clone' : true }" handle=".drag-handle">
          <TrelloBoardTask v-for="task in column.tasks" :key="task.id" :task="task" />
        </draggable>

        <footer>
          <button class="text-gray-500">+ Add a card</button>
        </footer>
      </div>
    </draggable>
  </div>
</template>

<script setup lang="ts">
import { nanoid } from "nanoid";
import { VueDraggableNext as draggable } from "vue-draggable-next";
import type { Column } from "~/types";

const ctrl = useKeyModifier("Control");

// not necessary to import ref from vue due to nuxt!
const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: "Backlog",
    tasks: [
      {
        id: nanoid(),
        title: "Create landing page",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Write some tests",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Learn Laravel Queues",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Svelte and stuff",
        createdAt: new Date(),
      },
    ],
  },
  {
    id: nanoid(),
    title: "In Progress",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Not Started",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Completed",
    tasks: [],
  },
]);
</script>

<style scoped>
/* .sortable-chosen { */
/*   background-color: green; */
/* } */

.sortable-drag {
  transform: rotate(5deg);
}

.sortable-ghost {
  @apply bg-slate-300 text-transparent;
}
</style>
