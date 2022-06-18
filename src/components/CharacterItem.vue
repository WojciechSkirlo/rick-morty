<template>
  <div class="flex flex-col border border-black">
    <div class="relative overflow-hidden h-96 group bg-slate-200 img">
      <img :src="item.image" class="object-cover w-full h-full transition-transform duration-200 group-hover:scale-105"
        @error="this.src = '/image_not_supported.svg'" />
      <div class="absolute left-0 flex flex-col items-start max-w-[90%] gap-2 bottom-4">
        <BaseBadge v-if="item.type" :value="item.type" :bg-color="1">type:</BaseBadge>
        <BaseBadge v-if="item.created" :value="item.created">created:</BaseBadge>
      </div>
    </div>
    <div class="relative flex flex-col p-4 pt-8 overflow-hidden text-sm">
      <div class="absolute top-0 left-0 z-0 w-full h-full transition-transform duration-200 -translate-y-full bg-black">
      </div>

      <div class="relative z-10 flex flex-col">
        <div class="flex items-center max-w-full gap-1">
          <span class="text-xs whitespace-nowrap first-letter:uppercase">
            Name:
          </span>
          <span class="font-medium truncate text-violet-300 first-letter:uppercase">
            {{ item.name }}
          </span>
        </div>
        <div class="flex items-center max-w-full gap-1">
          <span class="text-xs whitespace-nowrap first-letter:uppercase">
            Status:
          </span>
          <span class="font-medium truncate first-letter:uppercase">
            {{ item.status }}
          </span>
        </div>
        <div class="flex items-center max-w-full gap-1">
          <span class="text-xs whitespace-nowrap first-letter:uppercase">
            Species:
          </span>
          <span class="font-medium truncate first-letter:uppercase">
            {{ item.species }}
          </span>
        </div>
        <div class="flex items-center max-w-full gap-1">
          <span class="text-xs whitespace-nowrap first-letter:uppercase">
            Genger:
          </span>
          <span class="font-medium truncate first-letter:uppercase">
            {{ item.gender }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import BaseBadge from "../components/BaseBadge.vue"
defineProps({
  item: {
    type: Object,
    default() {
      return {}
    }
  }
})
</script>
<style scoped>
.img:hover+div>div:first-of-type {
  @apply translate-y-0;
}

.img:hover+div>div:nth-of-type(2) {
  @apply text-white;
}
</style>