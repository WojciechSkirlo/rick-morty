<template>
  <div class="flex items-center max-w-full gap-1 px-2 py-1 text-sm leading-4 text-white"
    :class="bgColor === 0 ? 'bg-black' : 'bg-violet-300'" :title="value">
    <span class="text-xs whitespace-nowrap first-letter:uppercase">
      <slot />
    </span>
    <span class="font-medium truncate first-letter:uppercase">{{ value }}</span>
  </div>
</template>
<script setup>
defineProps({
  value: {
    type: [Number, String],
    default: "",
  },

  bgColor: {
    type: Number,
    default: 0,
  }
})
</script>