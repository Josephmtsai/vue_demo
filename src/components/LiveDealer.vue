<template>
  <div
    class="w-screen flex justify-center items-center flex-wrap"
    v-on:click="movePosition($event)"
  >
    <div
      class="mt-[100px] w-full flex justify-center items-center cursor-pointer"
    >
      <div
        class="flex font-bold w-[960px] h-[80px] flex-row justify-center shadow-lg shadow-green-900"
      >
        <div
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
        >
          BP
        </div>
        <div
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
        >
          P
        </div>
        <div
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
        >
          PP
        </div>
      </div>
    </div>

    <div
      class="mt-[250px] w-full flex justify-center items-center cursor-pointer"
    >
      <div
        class="flex w-[960px] h-[100px] flex-row shadow-lg shadow-green-900 font-bold bg-green-800"
      >
        <div
          class="rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 hover:bg-green-400"
        >
          10
        </div>
        <div
          class="rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 hover:bg-green-400"
        >
          10
        </div>
        <div
          class="rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 hover:bg-green-400"
        >
          20
        </div>
        <div
          class="rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 hover:bg-green-400"
        >
          30
        </div>
        <div
          class="rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 hover:bg-green-400"
        >
          40
        </div>
        <div
          class="rounded-full border-2 h-[80px] border-white text-white w-[80px] p-5 flex justify-center items-center ml-3 hover:bg-green-400"
        >
          50
        </div>
      </div>
    </div>
  </div>
  <div
    class="w-[50px] h-[50px] absolute clickCircle"
    v-bind:style="{ top: yPosition, left: xPosition }"
  ></div>
</template>
<script setup lang="ts">
import { ref } from 'vue';

const xPosition = ref('0px');
const yPosition = ref('0px');
function movePosition(event: any) {
  xPosition.value = (event.pageX - 25).toString() + 'px';
  yPosition.value = (event.pageY - 25).toString() + 'px';
}
</script>

<style scoped>
.clickCircle:active {
  box-sizing: border-box;
  border-style: solid;
  border-color: black;
  background-color: transparent;
  border-radius: 50%;
  animation: clickEffect 0.4s ease-out;
  z-index: 99999;
}

@keyframes clickEffect {
  0% {
    opacity: 1;
    width: 1em;
    height: 1em;
    margin-top: 25px;
    margin-left: 25px;
    border-width: 0.5em;
  }
  100% {
    opacity: 0.2;
    width: 5em;
    height: 5em;
    border-width: 0.03em;
  }
}
</style>
