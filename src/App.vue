<script setup>

import {ref} from "vue";

const tasks = ref([
  { name: 'Task 1', minutes: 60 },
  { name: 'Task 2', minutes: 75 },
  { name: 'Task 3', minutes: 90 },
  { name: 'Task 4', minutes: 105 }
]);

function removeTask(index) {
  tasks.value.splice(index, 1);
}

const showAddTaskModal = ref(false);
const newTaskName = ref('');
const newTaskTime = ref(0);


const addTask = () => {
  if (newTaskName.value && newTaskTime.value) {
    tasks.value.push({
      name: newTaskName.value,
      minutes: newTaskTime.value, // Change this line to use 'minutes' instead of 'time'
    });
    newTaskName.value = '';
    newTaskTime.value = 0;
    showAddTaskModal.value = false;
  }
};


</script>

<template>

  <div id="app" class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Tasks</h1>

    <ul class="list-disc list-inside">
      <li v-for="(task, index) in tasks" :key="index" class="mb-2 flex items-center justify-between">
        <span>{{ task.name }} ({{ task.minutes }} minutes)</span>
        <button @click="removeTask(index)" class="bg-red-500 hover:bg-red-700 text-white font-bold py-1 px-3 rounded">
          Remove
        </button>
      </li>
    </ul>

    <button @click="showAddTaskModal = true" class="mt-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
      Add Task
    </button>

    <div v-if="showAddTaskModal" class="fixed z-50 inset-0 overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
      <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
        <div class="relative inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full">
          <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
            <div class="sm:flex sm:items-start">
              <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                <h3 class="text-lg leading-6 font-medium text-gray-900" id="modal-title">Add Task</h3>
                <div class="mt-4">
                  <form @submit.prevent="addTask">
                    <div class="mb-4">
                      <label for="task-name" class="block text-gray-700 font-bold mb-2">Task Name:</label>
                      <input type="text" id="task-name" v-model="newTaskName" class="w-full px-3 py-2 border rounded-md focus:outline-none focus:ring focus:border-blue-500" placeholder="Enter task name">
                    </div>
                    <div class="mb-4">
                      <label for="task-time" class="block text-gray-700 font-bold mb-2">Time (minutes):</label>
                      <input type="number" id="task-time" v-model="newTaskTime" class="w-full px-3 py-2 border rounded-md focus:outline-none focus:ring focus:border-blue-500" placeholder="Enter task time">
                    </div>
                    <button type="submit" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
                      Add Task
                    </button>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
            <button type="button" class="w-full inline-flex justify-center rounded-full border border-transparent shadow-sm px-4 py-2 bg-blue-500 text-base font-medium text-white hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 sm:ml-3 sm:w-auto sm:text-sm" @click="showAddTaskModal = false">
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<style scoped>

</style>
