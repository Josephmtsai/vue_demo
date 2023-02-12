<template>
  <div
    class="w-screen flex justify-center items-center flex-wrap"
    v-on:click="movePosition($event)"
  >
    <div
      class="mt-[100px] w-[960px] min-w-[480px] flex justify-center flex-wrap items-center cursor-pointer p-[2px] bg-yellow-800"
    >
      <div
        class="flex font-bold w-[960px] min-w-[480px] h-[80px] flex-row justify-center shadow-lg shadow-green-900 bg-yellow-800 gap-[2px] first:mt-0 mt-[2px]"
      >
        <div
          id="bp_bet"
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet('#bp_bet')"
        >
          BP
        </div>
        <div
          id="t_bet"
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet('#t_bet')"
        >
          T
        </div>
        <div
          id="pp_bet"
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet('#pp_bet')"
        >
          PP
        </div>
      </div>
      <div
        class="flex font-bold w-[960px] min-w-[480px] h-[80px] flex-row justify-center shadow-lg shadow-green-900 bg-yellow-800 gap-[2px] first:mt-0 mt-[2px]"
        v-on:click="placeBet('#b_bet')"
      >
        <div
          id="b_bet"
          class="flex-grow w-1/2 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
        >
          B
        </div>
        <div
          id="p_bet"
          class="flex-grow w-1/2 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet('#p_bet')"
        >
          P
        </div>
      </div>
    </div>

    <div
      ref="mybets"
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
  <!--Static Bets-->
  <div v-for="bet in betsSetting">
    <div v-if="bet.display">
      <Teleport :to="bet.id" :disabled="!bet.display">
        <Bets></Bets>
      </Teleport>
    </div>
  </div>
  <!--Transition animation--->
  <Transition
    v-on:before-enter="onBeforeEnter"
    v-on:enter="enter"
    v-on:after-enter="onAfterEnter"
    :css="false"
  >
    <Bets v-show="moveEvent"></Bets>
  </Transition>
</template>
<script setup lang="ts">
import gsap from 'gsap';
import { ref } from 'vue';
import Bets from './Bets.vue';
import type { Ref } from 'vue';
interface BetsInterface {
  display: boolean;
  id: string;
}

const betsSetting: Ref<BetsInterface[]> = ref([
  { display: false, id: '#bp_bet' },
  { display: false, id: '#p_bet' },
  { display: false, id: '#pp_bet' },
  { display: false, id: '#t_bet' },
  { display: false, id: '#b_bet' },
]);
const mybets: Ref<any> = ref(null);
const moveEvent: Ref<boolean> = ref(false);
const xPosition: Ref<string> = ref('0px');
const yPosition: Ref<string> = ref('0px');
function movePosition(event: any) {
  xPosition.value = (event.pageX - 25).toString() + 'px';
  yPosition.value = (event.pageY - 25).toString() + 'px';
  moveEvent.value = true;
}
function placeBet(id: string) {
  betsSetting.value.forEach((setting) => {
    if (setting.id === id) setting.display = true;
  });
}

function onBeforeEnter(el: any) {
  debugger;
  gsap.set(el, {
    x: 800,
    y: 800,
    opacity: 0,
  });
}

function enter(el: any, done: any) {
  gsap.to(el, {
    duration: 1,
    opacity: 1,
    x: 400,
    y: 400,
    onComplete: done,
  });
}

// called when the enter transition has finished.
function onAfterEnter(el: any) {
  gsap.to(el, {
    opacity: 0,
    x: 100,
    y: 100,
  });
  moveEvent.value = false;
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
    transform: scale(0.8);
    border-width: 0.5em;
  }
  100% {
    opacity: 0.2;
    transform: scale(2);
    border-width: 0.03em;
  }
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s linear;
  opacity: 1;
}
.fade-enter-to,
.fade-leave {
  opacity: 1;
}
</style>
