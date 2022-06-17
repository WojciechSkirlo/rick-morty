<template>
  <div class="w-full pb-12">
    <div class="container flex justify-center px-4 mx-auto xl:max-w-6xl">
      <div class="flex items-center gap-4">
        <button v-if="totalPages > 1" class="p-2 hover:underline first-letter:uppercase"
          :class="activePage === 1 && 'text-gray-400'" :disabled="activePage === 1"
          @click="$emit('update:activePage', activePage - 1)">left</button>
        <div class="flex items-center gap-2">
          <div v-for="item in listPagination" :key="item">
            <button v-if="!isNaN(item)" class="px-3 py-1 min-w-[2rem] text-white"
              :class="item === activePage ? 'bg-violet-300' : 'bg-black'" @click="$emit('update:activePage', item)">
              {{ item }}
            </button>
            <div v-else class="px-3 py-1 min-w-[2rem] text-white bg-black">
              ...
            </div>
          </div>
        </div>
        <button v-if="totalPages > 1" class="p-2 hover:underline first-letter:uppercase"
          :class="activePage === totalPages && 'text-gray-400'" :disabled="activePage === totalPages"
          @click="$emit('update:activePage', activePage + 1)">right</button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { reactive } from "@vue/reactivity"
import { onMounted } from "@vue/runtime-core";
import { list } from "postcss";

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

const paginationSize = reactive(5);
const listPagination = reactive([]);


function buildPagination() {
  if (props.totalPages <= paginationSize) {
    for (let i = 1; i <= props.totalPages; i++) {
      listPagination.push(i);
    }
  } else {
    if (props.activePage === 1) {
      for (let i = 1; i <= paginationSize - 2; i++) {
        listPagination.push(i);
      }
    } else if (props.activePage !== props.totalPages) {
      for (let i = 1; i <= props.totalPages; i++) {
        if (i % 2 == 0) {
          listPagination.push(i - 1);
        } else {
          listPagination.push(i + 1);
        }
      }
    }

    listPagination.push("...");
    listPagination.push(props.totalPages);
  }

  console.log("My pagination", listPagination);
}

onMounted(() => {
  buildPagination();
})
</script>