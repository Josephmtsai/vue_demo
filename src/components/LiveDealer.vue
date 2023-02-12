<template>
  <div
    class="w-screen flex justify-center items-center flex-wrap z-10"
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
          v-on:click="placeBet($event, '#bp_bet')"
        >
          BP

          <Bets
            v-for="index in 5"
            :key="index"
            class="z-[-1]"
            :id="'bp_chip' + index"
          ></Bets>
        </div>
        <div
          id="t_bet"
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet($event, '#t_bet')"
        >
          T
          <Bets
            v-for="index in 5"
            :key="index"
            class="z-[-1]"
            :id="'t_chip' + index"
          ></Bets>
        </div>
        <div
          id="pp_bet"
          class="flex-grow w-1/3 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet($event, '#pp_bet')"
        >
          PP
          <Bets
            v-for="index in 5"
            :key="index"
            class="z-[-1]"
            :id="'pp_chip' + index"
          ></Bets>
        </div>
      </div>
      <div
        class="flex font-bold w-[960px] min-w-[480px] h-[80px] flex-row justify-center shadow-lg shadow-green-900 bg-yellow-800 gap-[2px] first:mt-0 mt-[2px]"
      >
        <div
          id="b_bet"
          class="flex-grow w-1/2 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet($event, '#b_bet')"
        >
          B
          <Bets
            v-for="index in 5"
            :key="index"
            class="z-[-1]"
            :id="'b_chip' + index"
          ></Bets>
        </div>
        <div
          id="p_bet"
          class="flex-grow w-1/2 flex justify-center items-center text-white gap-2 bg-green-800 hover:bg-green-400"
          v-on:click="placeBet($event, '#p_bet')"
        >
          P
          <Bets
            v-for="index in 5"
            :key="index"
            class="z-[-1]"
            :id="'p_chip' + index"
          ></Bets>
        </div>
      </div>
    </div>

    <!--hidden bets-->
    <div class="mt-[240px] w-full flex justify-center items-center">
      <div ref="chip" class="w-[80px] h-[80px]">&nbsp;</div>
    </div>
    <div
      class="mt-[50px] w-full flex justify-center items-center cursor-pointer"
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
    class="w-[50px] h-[50px] absolute clickCircle z-[-1]"
    v-bind:style="{ top: yPosition, left: xPosition }"
  ></div>

  <!--Static Bets-->
  <div v-for="bet in betsSetting">
    <div v-if="bet.display">
      <Teleport :to="bet.id" :disabled="!bet.display">
        <Bets class="absolute t-[300px] l-[300px]"></Bets>
      </Teleport>
    </div>
  </div>
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
const betsItem: Ref<number> = ref(5);
const chip: Ref<any> = ref(null);
const xPosition: Ref<string> = ref('0px');
const yPosition: Ref<string> = ref('0px');
async function movePosition(event: any) {
  xPosition.value = (event.pageX - 25).toString() + 'px';
  yPosition.value = (event.pageY - 25).toString() + 'px';
  console.log('trigger');
}
function placeBet(event: any, id: string) {
  betsSetting.value.forEach((setting) => {
    if (setting.id === id) setting.display = true;
  });
  console.log(event.target.getBoundingClientRect());
  console.log(chip.value.getBoundingClientRect());
  const yValue =
    chip.value.getBoundingClientRect().y -
    event.target.getBoundingClientRect().y -
    event.target.getBoundingClientRect().height / 2 +
    chip.value.getBoundingClientRect().height / 2;
  const xValue =
    chip.value.getBoundingClientRect().x -
    event.target.getBoundingClientRect().x -
    event.target.getBoundingClientRect().width / 2 +
    chip.value.getBoundingClientRect().width / 2;
  let delay = 0;
  for (let i = 1; i <= betsItem.value; i++) {
    gsap.fromTo(
      id.replace('_bet', '_chip') + i.toString(),
      {
        duration: 0.1,
        delay: delay,
        opacity: 1,
        x: xValue,
        y: yValue,
        zIndex: 100,
      },
      {
        duration: 0.1,
        delay: delay,
        opacity: 1,
        x: 0,
        y: 0,
        zIndex: 0,
      }
    );
    delay = delay + 0.05;
  }
}
</script>

<style scoped>
.clickCircle:active {
  box-sizing: border-box;
  border-style: solid;
  border-color: black;
  background-color: transparent;
  border-radius: 50%;
  z-index: 100;
  animation: clickEffect 0.4s ease-out;
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
</style>
