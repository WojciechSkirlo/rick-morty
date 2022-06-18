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
        <div v-if="isFilters" class="flex flex-col justify-between w-full gap-4 p-4 mt-4 bg-violet-300">
          <form
            @submit.prevent="$emit('update:filters', { filtersParam: { query: 'status', value: vStatus.value } }); isFilters = false"
            class="flex flex-col gap-4">
            <div class="relative flex flex-col">
              <span class="mb-1.5 first-letter:uppercase">status</span>
              <div class="flex flex-col gap-1 p-4 bg-slate-200">
                <div v-for="item in vStatusOptions" :key="item.id" class="flex items-center gap-2">
                  <BaseRadioInput v-model:current-status="vStatus" :item="item" name="status" />
                </div>
              </div>
            </div>
            <div class="flex items-center justify-between gap-4">
              <BaseButton @click="$emit('update:filters', { filtersParam: {} }); vStatus = {}; ">wyczysc
              </BaseButton>
              <BaseButton type-button="submit">zastosuj</BaseButton>
            </div>
          </form>
        </div>
      </Transition>
    </div>
  </div>
</template>
<script setup>
import BaseButton from "../components/BaseButton.vue"
import BaseRadioInput from "../components/BaseRadioInput.vue";
import { ref } from "@vue/reactivity";

const props = defineProps({
  filters: {
    type: Object,
    default() {
      return {}
    }
  }
})

const isFilters = ref(false)

const vStatus = ref({});
const vStatusOptions = ref([
  { id: 1, value: 'alive', text: 'Alive' },
  { id: 2, value: 'dead', text: 'Dead' },
  { id: 3, value: 'unknown', text: 'Unknown' },
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