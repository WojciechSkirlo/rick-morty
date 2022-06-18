<template>
  <div class="w-full pb-12">
    <div class="container flex justify-center px-4 mx-auto xl:max-w-6xl">
      <div class="flex items-center gap-4">
        <button v-if="totalPages > 1" class="p-2 hover:underline first-letter:uppercase"
          :class="activePage === 1 && 'text-gray-400'" :disabled="activePage === 1"
          @click="$emit('update:activePage', { page: activePage - 1 })">left</button>
        <div class="flex items-center gap-2">
          <div v-for="item in computedPagination" :key="item">
            <button v-if="!isNaN(item)" class="px-3 py-1 min-w-[2rem] text-white"
              :class="item === activePage ? 'bg-violet-300' : 'bg-black'"
              @click="$emit('update:activePage', { page: item })">
              {{ item }}
            </button>
            <div v-else class="px-3 py-1 min-w-[2rem] text-white bg-black">
              ...
            </div>
          </div>
        </div>
        <button v-if="totalPages > 1" class="p-2 hover:underline first-letter:uppercase"
          :class="activePage === totalPages && 'text-gray-400'" :disabled="activePage === totalPages"
          @click="$emit('update:activePage', { page: activePage + 1 })">right</button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { computed } from "@vue/runtime-core";

defineEmits(["update:activePage"])

const props = defineProps({
  activePage: {
    type: Number,
    default: 0,
  },

  totalPages: {
    type: Number,
    default: 0,
  }
})

const computedPagination = computed(() => {
  let paginationTab = [];
  if (props.totalPages <= 5) {
    for (let i = 1; i <= props.totalPages; i++) {
      paginationTab.push(i);
    }
  } else {
    if (props.activePage >= props.totalPages - 1) {
      paginationTab.push(1);
      paginationTab.push("...");
    }


    for (let i = props.activePage - 1; i <= props.activePage + 1; i++) {
      props.activePage === props.totalPages && i === props.totalPages - 1 && paginationTab.push(i - 2);
      i !== 0 && i !== props.totalPages + 1 && paginationTab.push(i)
      props.activePage === 1 && i === 2 && paginationTab.push(i + 1);
    }

    if (props.activePage < props.totalPages - 1) {
      paginationTab.push("...");
      paginationTab.push(props.totalPages);
    }
  }

  return paginationTab;
})

</script>