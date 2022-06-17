<template>
  <div class="w-full pt-8">
    <div v-if="listCharacters.value"
      class="container grid grid-cols-1 gap-2 px-2 mx-auto sm:px-4 sm:grid-cols-2 md:grid-cols-3 xl:max-w-6xl xl:grid-cols-4 gap-y-6">
      <div v-for="item in listCharacters.value" :key="item.id">
        <CharacterItem :item="item"></CharacterItem>
      </div>
    </div>
  </div>
</template>
<script setup>
import CharacterItem from "../components/CharacterItem.vue"
import { reactive, onMounted } from 'vue';

const listCharacters = reactive([]);

function getCharacters() {
  fetch(`https://rickandmortyapi.com/api/character`)
    .then((res) => res.json())
    .then((data) => {
      listCharacters.value = data.results;

      console.log({ listCharacters });
    });
}

onMounted(() => {
  getCharacters();
})
</script>