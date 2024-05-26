<script setup>
import { ref } from 'vue';
const statuses = ref(['alive', 'dead', 'unknown']);
const emit = defineEmits(['search']);

const name = ref('');
const status = ref('');

const search = () => {
  emit('search', { name: name.value, status: status.value });
};
</script>

<template>
  <form class="max-w-lg mx-auto flex items-center space-x-2 mt-5">
    <h2>Фильтр</h2>
    <div>
      <input
        v-model="name"
        type="text"
        class="bg-gray-50 flex-1 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        placeholder="имя"
        required
      />
    </div>
    <select
      v-model="status"
      id="countries"
      class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
    >
      <option selected>Выбрать статус</option>
      <option v-for="status in statuses">{{ status }}</option>
    </select>
    <button
      @click="search"
      type="button"
      class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
    >
      Поиск
    </button>
  </form>
</template>
