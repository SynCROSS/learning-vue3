<script setup lang="ts">
import { reactive, ref } from 'vue';

const message = ref('Hello, world');
const counter = reactive({ count: 0 });

</script>

<template>
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
</template>
