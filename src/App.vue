<script setup>
import Clock from "./components/Clock.vue";
</script>

<template>
  <div
    class="bg-gradient-to-r from-cyan-500 to-blue-500 h-screen max-h-screen text-white">
    <Clock />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
