<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);
</script>

<template>
  <!-- make this button work -->
  <button @click="count++">
    count is: {{ count }}
  </button>
</template>
