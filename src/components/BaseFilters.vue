<template>
  <div class="w-full pt-8">
    <div class="container px-4 mx-auto xl:max-w-6xl">
      <div class="flex justify-end w-full">
        <button @click="isFilters = !isFilters"
          class="p-2 text-white transition-all bg-slate-200 outline-2 outline-violet-300">
          <img src="/tune_FILL0_wght200_GRAD0_opsz48.svg" alt="" class="w-6 h-6">
        </button>
      </div>
      <Transition name="slide">
        <div v-if="isFilters" class="flex flex-col justify-between w-full gap-4 p-4 mt-4 h-60 bg-violet-300">
          <div class="flex gap-4">
            <BaseSelect v-model="vStatus" label="Status" :options="vStatusOptions" />
            <BaseSelect v-model="vGender" label="Gender" :options="vGenderOptions" />
          </div>
          <button class="first-letter:uppercase self-end px-6 py-1.5 bg-black text-white">zastosuj</button>
        </div>
      </Transition>
    </div>
  </div>
</template>
<script setup>
import BaseSelect from "../components/BaseSelect.vue"
import { reactive, ref } from "@vue/reactivity";

const isFilters = ref(true)

const vStatus = ref({ id: 1, value: 'alive', text: 'Alive' });
const vStatusOptions = ref([
  { id: 1, value: 'alive', text: 'Alive' },
  { id: 2, value: 'dead', text: 'Dead' },
  { id: 3, value: 'unknown', text: 'Unknown' },
])

const vGender = ref({ id: 1, value: 'female', text: 'Female' });
const vGenderOptions = ref([
  { id: 1, value: 'female', text: 'Female' },
  { id: 2, value: 'male', text: 'Male' },
  { id: 3, value: 'genderless', text: 'Genderless' },
  { id: 4, value: 'unknown', text: 'Unknown' },
])

</script>
<style scoped>
.slide-enter-from,
.slide-leave-to {
  @apply opacity-0;
}

.slide-enter-active,
.slide-leave-active {
  @apply transition-all duration-300
}
</style>