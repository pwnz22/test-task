<script setup>
import { ref, computed } from 'vue';

const emit = defineEmits(['change-page']);

const changePage = (page) => {
  current.value = page;
  emit('change-page', page);
};

const props = defineProps({
  pagination: {
    type: Object,
    required: true,
  },
});

const current = ref(1);
const pageSidesRange = ref(5);

const pages = computed(() => {
  let pages = [];

  for (let i = rangeStart.value; i <= rangeEnd.value; i++) {
    pages.push(i);
  }

  return pages;
});

const rangeStart = computed(() => {
  let start = current.value - pageSidesRange.value;
  return start > 0 ? start : 1;
});

const rangeEnd = computed(() => {
  let end = current.value + pageSidesRange.value;
  return end < props.pagination.pages ? end : props.pagination.pages;
});

const nextPage = computed(() => {
  return current.value + 1;
});
const prevPage = computed(() => {
  return current.value - 1;
});
const hasPrev = computed(() => {
  return current.value > 1;
});
const hasNext = computed(() => {
  return current.value < props.pagination.pages;
});
</script>

<template>
  <nav class="flex justify-center mt-5">
    <ul class="flex items-center -space-x-px h-10 text-base">
      <li>
        <button
          @click.prevent="changePage(prevPage)"
          :disabled="!hasPrev"
          class="disabled:opacity-20 flex items-center justify-center px-4 h-10 ms-0 leading-tight text-gray-500 bg-white border border-e-0 border-gray-300 rounded-s-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
        >
          <span class="sr-only">Previous</span>
          <svg
            class="w-3 h-3 rtl:rotate-180"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 6 10"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M5 1 1 5l4 4"
            />
          </svg>
        </button>
      </li>
      <li v-for="page in pages">
        <button
          @click="changePage(page)"
          :class="[
            current == page
              ? 'z-10 text-blue-600 border-blue-300 hover:bg-blue-100 bg-blue-50'
              : 'border-gray-300 hover:bg-gray-100 text-gray-500 bg-white',
          ]"
          class="flex items-center justify-center px-4 h-10 leading-tight border hover:text-gray-700"
        >
          {{ page }}
        </button>
      </li>

      <li>
        <button
          @click.prevent="changePage(nextPage)"
          :disabled="!hasNext"
          class="disabled:opacity-20 flex items-center justify-center px-4 h-10 leading-tight text-gray-500 bg-white border border-gray-300 rounded-e-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
        >
          <span class="sr-only">Next</span>
          <svg
            class="w-3 h-3 rtl:rotate-180"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 6 10"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="m1 9 4-4-4-4"
            />
          </svg>
        </button>
      </li>
    </ul>
  </nav>
</template>
