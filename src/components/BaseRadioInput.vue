<template>
  <label class="flex items-center gap-3">
    <input type="radio" :name="name" :value="item.id" class="hidden" :checked="currentStatus.id === item.id"
      @input="$emit('update:currentStatus', item)">
    <div class="flex items-center justify-center w-5 h-5 bg-white border border-black cursor-pointer">
      <div class="hidden w-3 h-3 bg-black"></div>
    </div>
    <span class="first-letter:uppercase">{{ item.text }}</span>
  </label>
</template>
<script setup>
const props = defineProps({
  currentStatus: {
    type: Object,
    default() {
      return {};
    }
  },

  item: {
    type: Object,
    default() {
      return {};
    }
  },

  name: {
    type: String,
    default: "",
  }
})
</script>
<style scoped>
label>input:checked+div>div {
  @apply block;
}
</style>