<template>
  <div class="container mx-auto">
    <h1 class="mt-8 text-2xl">Tasks</h1>

    <div class="mt-3">
      <div class="grid grid-cols-12 gap-4">
        <div class="col-span-6 space-y-4 px-1"
             style="height: 500px">
          <div
              v-for="(task, index) in tasks"
              :key="index"
              class="p-8 bg-white shadow-md rounded flex items-center justify-between">
            <div>
              <div>{{ task.text }}</div>
              <div class="text-gray-500 text-sm">
                {{ task.createdAt.toString() }}
              </div>
            </div>
            <div class="space-x-2">
              <button 
                class="px-2 text-red-600"
                title="Remove todo"
              >
                &times;
              </button>
              <button
                class="px-2 text-green-600"
                title="Mark as done"
              >
                &check;
              </button>
              <button
                class="px-2 text-orange-600"
                title="Mark as undone"
              >
                &#8630;
              </button>
            </div>
          </div>
          <div
            class="px-8 py-16 bg-white text-gray-700 shadow-md rounded text-sm"
          >
            No tasks found.
          </div>
        </div>

        <div class="col-span-6">
          <div class="p-8 bg-white shadow-md rounded">
            <h2 class="text-xl">Add Task</h2>
            <input 
              type="text"
              v-model="taskText"
              @keydown.enter="addTask"
              class="p-2 mt-4 border rounded w-full"
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, reactive, ref } from 'vue';

export default defineComponent({
  setup() {
    const tasks = reactive([]);
    const taskText = ref("");

    function addTask() {
      tasks.unshift({
        text: taskText.value,
        createdAt: new Date(),
        completed: false
      });

      taskText.value = "";
    }

    return {
      tasks,
      taskText,
      addTask
    }
  }
});
</script>