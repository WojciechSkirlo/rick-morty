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
        <div v-if="isFilters" class="w-full h-40 mt-4 bg-violet-300"></div>
      </Transition>
    </div>
  </div>
</template>
<script setup>
import { ref } from "@vue/reactivity";

const isFilters = ref(false)
</script>
<style scoped>
.slide-enter-from,
.slide-leave-to {
  @apply h-0 mt-0;
}

.slide-enter-active,
.slide-leave-active {
  @apply transition-all duration-300
}
</style>