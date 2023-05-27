<script lang="ts" setup>
import { defineModel } from "vue";

const modelValue = defineModel();
</script>

<template>
  <div class="w-[200] h-[200] bg-slate-400 p-4">
    <p>Hello Component 2</p>
    <input type="text" v-model="modelValue" />
  </div>
</template>
