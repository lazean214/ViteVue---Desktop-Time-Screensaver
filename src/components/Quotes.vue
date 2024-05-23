<template>
  <div class="absolute right-9 bottom-9 w-[350px] font-bold">
    <p>
      "{{ randomQuote }}" <br />
      <span class="underline">
        {{ randomAuthor }}
      </span>
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const randomQuote = ref("");
const randomAuthor = ref("");

const config = {
  apiUrl: "https://api.quotable.io/random",
};

const fetchRandomQuote = async () => {
  try {
    const response = await fetch(config.apiUrl);
    const data = await response.json();
    randomQuote.value = data.content;
    randomAuthor.value = data.author;
    console.log(data);
  } catch (error) {
    console.error("Failed to fetch random quote:", error);
  }
};

onMounted(() => {
  // Fetch random quote immediately
  fetchRandomQuote();

  // Fetch a new random quote every minute
  const intervalId = setInterval(fetchRandomQuote, 60000);

  // Cleanup interval on component unmount
  onUnmounted(() => clearInterval(intervalId));
});
</script>
