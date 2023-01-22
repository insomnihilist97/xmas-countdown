<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { computed } from 'vue';

const msToDays = 86400000;
const msToHours = 3600000;
const msToMinutes = 60000;
const now = useNow();
const useNowArr = String(now.value).split(' ');
let pastCurrentYearChristmas = false;
if(useNowArr[1] === 'Dec' && useNowArr[2] >= 25)
  pastCurrentYearChristmas = true;
const christmas = pastCurrentYearChristmas ? new Date('12/25/' + (useNowArr[3] + 1) +  ' 00:00:00') 
  : new Date('12/25/' + useNowArr[3] + ' 00:00:00');
const timeBeforeMs = computed(() => {
  return christmas - now.value;
});
const daysUntil = computed(() => {
  return Math.trunc(timeBeforeMs.value / msToDays);
})
const hoursUntil = computed(() => {
  return Math.trunc((timeBeforeMs.value % msToDays) / msToHours);
})
const minsUntil = computed(() => {
  return Math.trunc(((timeBeforeMs.value % msToDays) % msToHours) / msToMinutes);
})
const secsUntil = computed(() => {
  return Math.trunc((((timeBeforeMs.value % msToDays) % msToHours) % msToMinutes) / 1000);
})

</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number=daysUntil />
          <CountdownSegment label="hours" :number=hoursUntil />
          <CountdownSegment label="minutes" :number=minsUntil />
          <CountdownSegment label="seconds" :number=secsUntil />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
