<template>
  <button class="first-letter:uppercase self-start px-6 py-1.5 bg-black text-white" :type="typeButton">
    <slot />
  </button>
</template>
<script setup>
const props = defineProps({
  typeButton: {
    type: String,
    default: "button"
  }
})
</script>