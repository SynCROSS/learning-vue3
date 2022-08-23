<script setup lang="ts">
import { ref } from 'vue';

const awesome = ref(true);

const toggle = () => {
  awesome.value = !awesome.value;
};
</script>

<template>
  <button
    type="button"
    role="button"
    :aria-pressed="!awesome"
    @click="toggle"
  >
    toggle
  </button>
  <h1 v-if="awesome">
    Vue is awesome!
  </h1>
  <h1 v-else>
    Oh no 😢
  </h1>
</template>
