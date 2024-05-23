<script setup>
import Controls from "./Controls.vue";
import Quotes from "./Quotes.vue";
import { ref, onMounted } from "vue";

const currentTime = ref("");
const currentDate = ref("");

const updateTime = () => {
  const date = new Date();
  const hours = formatTime(date.getHours());
  const minutes = formatTime(date.getMinutes());
  const seconds = formatTime(date.getSeconds());

  currentTime.value = `${hours}:${minutes}`;
};

const updateDate = () => {
  const date = new Date();
  const dayOfWeek = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"][
    date.getDay()
  ];
  const day = formatTime(date.getDate());
  const month = formatTime(date.getMonth() + 1); // Note: January is 0
  const year = formatTime(date.getFullYear());
  currentDate.value = `${dayOfWeek}, ${day}.${month}.${year}`;
};

const formatTime = (time) => {
  return time < 10 ? `0${time}` : time;
};

onMounted(() => {
  updateTime();
  updateDate();
  setInterval(updateTime, 1000);
});
</script>

<template>
  <div>
    <Controls>
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
        <h1 class="font-bold drop-shadow-sm">
          {{ currentTime }}
        </h1>
        <h4
          class="absolute top-5 md:top-9 right-2 md:right-5 uppercase text-2xl">
          {{ currentDate }}
        </h4>
      </div>
      <Quotes />
    </Controls>
  </div>
</template>

<style scoped>
h1 {
  font-family: "Oswald", sans-serif;
  font-optical-sizing: auto;
  font-size: 10em;
}

@media screen and (min-width: 768px) {
  h1 {
    font-size: 15em;
  }
}
</style>
