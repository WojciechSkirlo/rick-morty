<template>
  <div class="relative flex flex-col">
    <span class="mb-1.5 text-xs first-letter:uppercase">default</span>
    <div @click="isOptions = !isOptions" class="flex items-center px-4 py-1.5 bg-slate-200 cursor-pointer">
      <input type="text" :value="modelValue.text" readonly
        class="font-medium bg-transparent outline-none cursor-pointer">
      <button :class="isOptions && 'rotate-180'" class="transition-transform duration-200">
        <img src="/expand_more.svg" alt="" class="w-6 h-6">
      </button>
    </div>
    <ul v-if="isOptions" class="absolute left-0 z-20 w-full top-full bg-slate-200">
      <li v-for="item in options" :key="item.id"
        class="px-4 py-1.5 text-sm hover:text-white hover:bg-black cursor-pointer"
        :class="item.id === modelValue.id && ['font-semibold']"
        @click="$emit('update:modelValue', item); isOptions = false">
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>
<script setup>
import { ref } from "@vue/reactivity";

defineEmits(["update:modelValue"])

const props = defineProps({
  modelValue: {
    type: Object,
    default() {
      return {}
    }
  },

  options: {
    type: Array,
    default() {
      return []
    }
  },

  label: {
    type: String,
    default: "",
  }
})

const isOptions = ref(false);
</script>