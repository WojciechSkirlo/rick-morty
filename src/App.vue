<template>
  <main>
    <BaseFilters />
    <CharacterList :list-characters="listCharacters.value" />
    <BasePagination v-if="totalPages" :active-page="activePage" :total-pages="totalPages"
      @update:active-page="getCharacters" />
  </main>
</template>

<script setup>
import BaseFilters from "./components/BaseFilters.vue"
import CharacterList from "./components/CharacterList.vue";
import BasePagination from "./components/BasePagination.vue";
import { ref } from "@vue/reactivity";
import { reactive, onMounted } from 'vue';

const activePage = ref(1);
const totalPages = ref(0);
const listCharacters = reactive([]);

function getCharacters(page = 1) {
  fetch(`https://rickandmortyapi.com/api/character/?page=${page}`)
    .then((res) => res.json())
    .then((data) => {
      listCharacters.value = data.results;
      totalPages.value = data.info.pages;
      activePage.value = page;
      window.scrollTo(0, 0);
    });
}

onMounted(() => {
  getCharacters();
})

</script>
