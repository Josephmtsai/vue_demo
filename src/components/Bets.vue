<template>
  <div
    class="absolute rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 bg-red-500 z-1 shadow-lg shadow-black"
    :class="classes"
  >
    Chip
  </div>
</template>

<script setup lang="ts">
interface Props {
  classes?: string;
}
defineProps<Props>();
</script>
