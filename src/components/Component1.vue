<script lang="ts" setup>
const modelValue = defineModel();
</script>

<template>
  <div class="@container h-full">
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 1</p>
      <input type="text" v-model="modelValue" />
    </div>
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 1</p>
      <input type="text" v-model="modelValue" />
    </div>
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 1</p>
      <input type="text" v-model="modelValue" />
    </div>
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 2</p>
      <input type="text" v-model="modelValue" />
    </div>
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 1</p>
      <input type="text" v-model="modelValue" />
    </div>
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 1</p>
      <input type="text" v-model="modelValue" />
    </div>
    <div class="bg-yellow-400 p-4 @md:bg-red-400">
      <p>Hello Component 1</p>
      <input type="text" v-model="modelValue" />
    </div>
  </div>
</template>
