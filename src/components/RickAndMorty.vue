<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const characters = ref([]);
const pagination = ref({});

onMounted(async () => {
  const { data } = await axios.get('https://rickandmortyapi.com/api/character');
  characters.value = data.results;
  pagination.value = data.info;
});

// const nextPage = () => {
//   if (page.value !== Math.ceil(pagination.value.info. / perPage)) {
//     page.value += 1;
//   }
// };

const backPage = () => {
  if (page.value !== 1) {
    page.value -= 1;
  }
};

const goToPage = (numPage) => {
  page.value = numPage;
};
</script>

<template>
  <div class="grid grid-cols-3 gap-5 max-w-3xl mx-auto mt-10">
    <div
      class="bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700"
      v-for="character in characters"
    >
      <a href="#">
        <img class="rounded-t-lg" :src="character.image" alt="" />
      </a>
      <div class="p-5">
        <a href="#">
          <h5
            class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
          >
            {{ character.name }}
          </h5>
        </a>
        <div class="flex space-x-2">
          <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
            {{ character.status }}
          </p>
          <span>-</span>
          <p>{{ character.species }}</p>
        </div>
        <h3 class="text-gray-400">First seen in:</h3>
        <p>{{ character.location.name }}</p>
      </div>
    </div>
  </div>
</template>
