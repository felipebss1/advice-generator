<template>
  <div class="w-11/12 mx-auto mt-11">
    <p class="text-[#52ffa8] text-center text-xs tracking-[4px] pb-6">
      ADVICE #{{ adviceID }}
    </p>
    <p class="text-[#cee3e9] text-center text-[1.55rem]">
      {{ `"${newAdvice}"` }}
    </p>
    <img
      src="/pattern-divider-mobile.svg"
      alt="divider pattern"
      class="mx-auto pt-6 md:hidden"
    />
    <img
      src="/pattern-divider-desktop.svg"
      alt="divider pattern"
      class="mx-auto pt-6 hidden md:block"
    />
  </div>
  <figure
    class="flex items-center mx-auto w-16 h-16 bg-[#52ffa8] rounded-full relative -bottom-8 cursor-pointer glow"
    @click="getAdvice"
  >
    <img src="/icon-dice.svg" alt="dice icon" class="mx-auto" />
  </figure>
</template>

<script setup>
import { ref } from "vue";
const newAdvice = ref("Press the dice button to generate an advice");
const adviceID = ref(0);

const getAdvice = async () => {
  const res = await fetch(`https://api.adviceslip.com/advice`);
  const data = await res.json();
  newAdvice.value = data.slip.advice;
  adviceID.value = data.slip.id;
};
</script>

<style scoped>
.glow:hover {
  filter: drop-shadow(0 0 1rem #52ffa8);
}
</style>
