<template>
  <main>
    <BaseFilters />
    <CharacterList />
    <BasePagination />
  </main>
</template>

<script setup>
import BaseFilters from "./components/BaseFilters.vue"
import CharacterList from "./components/CharacterList.vue";
import BasePagination from "./components/BasePagination.vue";
</script>
