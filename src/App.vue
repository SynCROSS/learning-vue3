<script setup lang="ts">
import { ref } from 'vue';

const titleClass = ref('title');
</script>

<template>
  <h1 :class="titleClass">
    Make me red
  </h1> <!-- add dynamic class binding here -->
</template>

<style>
.title {
  color: #ff1740;
}
</style>
