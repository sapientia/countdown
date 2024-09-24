<script setup>
import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "@/components/CountdownSegment.vue";
import { shallowRef, onMounted, onUnmounted } from "vue";

let days = shallowRef(0)
let hours = shallowRef(0)
let minutes = shallowRef(0)
let seconds = shallowRef(0)

// Convert date based on given day
const date = shallowRef('01/01/2025')
const [day, month, year] = date.value.split('/');
const dateObject = new Date(`${year}-${month}-${day}`);


//Get Miliseconds per Minute, Hour and Day
const millisecondsInSecond = 1000;
const millisecondsInMinute = millisecondsInSecond * 60;
const millisecondsInHour = millisecondsInMinute * 60;
const millisecondsInDay = millisecondsInHour * 24;

const calculateTimeRemaining = () => {
  //Get current Day
  const currentDate = new Date();

  // Get time difference in miliseconds
  const timeDifference = dateObject - currentDate;

  // Get time difference
  days.value = Math.floor(timeDifference / millisecondsInDay);
  hours.value = Math.floor((timeDifference % millisecondsInDay) / millisecondsInHour);
  minutes.value = Math.floor((timeDifference % millisecondsInHour) / millisecondsInMinute);
  seconds.value = Math.floor((timeDifference % millisecondsInMinute) / millisecondsInSecond);
  console.log(`Faltan ${days.value} días, ${hours.value} horas, ${minutes.value} minutos y ${seconds.value} segundos.`);
}


onMounted(() => {
  setInterval(calculateTimeRemaining, 1000); // Update every second
});

onUnmounted(() => clearInterval());

</script>
<template>
  <div class="app-wrapper">
    <div class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :number="days" />
        <CountdownSegment data-test="hours" label="hours" :number="hours" />
        <CountdownSegment data-test="minutes" label="minutes" :number="minutes" />
        <CountdownSegment data-test="seconds" label="seconds" :number="seconds" />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}

.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}

body {
  @apply bg-gray-100;
}
</style>
