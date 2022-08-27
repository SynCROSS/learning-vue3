<script setup lang="ts">
import { onMounted, ref } from 'vue';

const p = ref<HTMLParagraphElement>();

onMounted(() => {
  if (p.value?.textContent) {
    p.value.textContent += 'World!';
  }
});
</script>

<template>
  <p ref="p">
    Hello
  </p>
</template>
