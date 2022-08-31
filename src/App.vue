<script setup lang="ts">
import { ref } from 'vue';
import ChildComp from './components/ChildComp.vue';

const greeting = ref('Hello from parent');
</script>

<template>
  <ChildComp :msg="greeting" />
</template>
