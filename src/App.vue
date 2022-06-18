<template>
  <main>
    <BaseFilters @update:filters="getCharacters" />
    <CharacterList :list-characters="listCharacters" />
    <BasePagination v-if="totalPages" :active-page="activePage" :total-pages="totalPages"
      @update:active-page="getCharacters" />
  </main>
</template>

<script setup>
import BaseFilters from "./components/BaseFilters.vue"
import CharacterList from "./components/CharacterList.vue";
import BasePagination from "./components/BasePagination.vue";
import { ref } from "@vue/reactivity";
import { onMounted } from 'vue';

const activePage = ref(1);
const filters = ref({});
const totalPages = ref(0);
const listCharacters = ref([]);

function getCharacters({ page = 1, filtersParam = filters.value } = {}) {
  const checkFilters = Object.entries(filtersParam).length && filtersParam.value != undefined && filtersParam.query != undefined;
  if (activePage != page) {
    fetch(`https://rickandmortyapi.com/api/character/?page=${page}${checkFilters ? `&${filtersParam.query}=${filtersParam.value}` : ''}`)
      .then((res) => res.json())
      .then((data) => {
        listCharacters.value = data.results;
        totalPages.value = data.info.pages;
        activePage.value = page;
        filters.value = filtersParam;
        window.scrollTo(0, 0);
      });
  }
}

onMounted(() => {
  getCharacters();
})

</script>
