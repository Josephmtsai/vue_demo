<template>
  <div class="flex justify-center w-screen">
    <div class="mt-[100px]">
      <div
        class="flex w-[960px] h-[80px] flex-row justify-center border-green-600"
      >
        <div
          class="flex-grow first:border-l-2 w-1/3 last:border-r-2 border-t-2 border-b-2 border-green-600"
        >
          <span
            class="inline-block w-full h-full align-middle text-center p-[20px]"
            >BP</span
          >
        </div>
        <div
          class="flex-grow first:border-l-2 w-1/3 last:border-r-2 border-t-2 border-b-2 border-green-600"
        >
          <span
            class="inline-block w-full h-fullalign-middle text-center p-[20px]"
            >BP</span
          >
        </div>
        <div
          class="flex-grow first:border-l-2 w-1/3 last:border-r-2 border-t-2 border-b-2 border-green-600"
        >
          <span
            class="inline-block w-full h-full align-middle text-center p-[20px]"
            >BP</span
          >
        </div>
      </div>
      <div class="bg-green-400">Place Bet</div>
    </div>
  </div>
</template>
<script setup lang="ts"></script>

<style scoped>
.flex-item {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
</style>
