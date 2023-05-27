<script lang="ts" setup>
import { defineModel } from "vue";

const modelValue = defineModel();
</script>

<template>
  <div class="w-[200] h-[200] bg-yellow-400 p-4">
    <p>Hello Component 1</p>
    <input type="text" v-model="modelValue" />
  </div>
</template>
