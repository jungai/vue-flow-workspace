<script lang="ts" setup>
import type { Raw } from "vue";
import type { TComponent } from "../types";
import { defineModel, defineProps, markRaw } from "vue";
import Component1 from "./Component1.vue";
import Component2 from "./Component2.vue";

type TCustomNodeProps = {
  componentName: TComponent;
  id: string;
};

const { componentName, id } = defineProps<TCustomNodeProps>();

defineEmits<{
  close: [id: string];
}>();

const components: Record<TComponent, Raw<any>> = {
  Component1: markRaw(Component1),
  Component2: markRaw(Component2),
};

const modelValue = defineModel();
</script>

<template>
  <div
    class="relative w-[300px] h-[300px] p-4 flex flex-col bg-zinc-500 gap-y-4 rounded-lg ring-2 ring-offset-2 ring-pink-500"
  >
    <p class="text-white font-semibold">
      Component
      <span class="underline decoration-pink-500 italic text-2xl">
        {{ componentName }}
      </span>
    </p>
    <input type="text" v-model="modelValue" />
    <component :is="components[componentName]" />
    <button
      @click="$emit('close', id)"
      class="absolute -top-3 -right-3 border border-black rounded-full text-xs bg-black text-white h-8 w-8 flex justify-center items-center hover:opacity-50"
    >
      X
    </button>
  </div>
</template>
