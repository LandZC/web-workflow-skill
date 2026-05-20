<script setup>
import { ref } from 'vue';

const count = ref(0);
</script>

<template>
  <div class="min-h-screen flex flex-col items-center justify-center">
    <h1 class="text-4xl font-bold mb-4">Welcome to My Vue Project</h1>
    <p class="text-lg text-gray-600 mb-4">
      Edit <code class="bg-gray-100 px-2 py-1 rounded">src/App.vue</code> and save to reload.
    </p>
    <button
      @click="count++"
      class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
    >
      Count: {{ count }}
    </button>
  </div>
</template>
