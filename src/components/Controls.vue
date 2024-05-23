<script setup>
import { ref } from "vue";

const isFullscreen = ref(false);

const toggleFullscreen = () => {
  if (!isFullscreen.value) {
    enterFullscreen();
  } else {
    exitFullscreen();
  }
};

const enterFullscreen = async () => {
  const element = document.documentElement;
  try {
    await element.requestFullscreen();
    await navigator.wakeLock.request("screen"); // Request wake lock
  } catch (err) {
    console.error("Failed to enter fullscreen:", err);
    return;
  }
};

const exitFullscreen = async () => {
  try {
    await document.exitFullscreen();
    await navigator.wakeLock.release(); // Release wake lock
  } catch (err) {
    console.error("Failed to exit fullscreen:", err);
    return;
  }
};

document.addEventListener("fullscreenchange", () => {
  isFullscreen.value = !!document.fullscreenElement;
});
</script>

<template>
  <div>
    <div @click="toggleFullscreen" class="absolute top-0 right-0">
      <div v-if="!isFullscreen">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="3em"
          height="3em"
          viewBox="0 0 24 24">
          <path
            fill="currentColor"
            fill-rule="evenodd"
            d="M6 4.75c-.69 0-1.25.56-1.25 1.25v3a.75.75 0 0 1-1.5 0V6A2.75 2.75 0 0 1 6 3.25h3a.75.75 0 0 1 0 1.5zM14.25 4a.75.75 0 0 1 .75-.75h3A2.75 2.75 0 0 1 20.75 6v3a.75.75 0 0 1-1.5 0V6c0-.69-.56-1.25-1.25-1.25h-3a.75.75 0 0 1-.75-.75M4 14.25a.75.75 0 0 1 .75.75v3c0 .69.56 1.25 1.25 1.25h3a.75.75 0 0 1 0 1.5H6A2.75 2.75 0 0 1 3.25 18v-3a.75.75 0 0 1 .75-.75m16 0a.75.75 0 0 1 .75.75v3A2.75 2.75 0 0 1 18 20.75h-3a.75.75 0 0 1 0-1.5h3c.69 0 1.25-.56 1.25-1.25v-3a.75.75 0 0 1 .75-.75"
            clip-rule="evenodd" />
        </svg>
      </div>
    </div>
    <div ref="fullscreenElement">
      <slot></slot>
    </div>
  </div>
</template>
