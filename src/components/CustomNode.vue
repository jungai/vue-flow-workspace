<script lang="ts" setup>
import type { Component } from "vue";
import type { TComponent } from "../types";
import { defineAsyncComponent, computed, ref } from "vue";
import { NodeResizer } from "@vue-flow/node-resizer";
import type { OnResize } from "@vue-flow/node-resizer";
import type { Dimensions } from "@vue-flow/core";
import "@vue-flow/node-resizer/dist/style.css";

type TCustomNodeProps = {
  componentName: TComponent;
  id: string;
  dimensions?: Dimensions;
};

const { componentName, id, dimensions } = defineProps<TCustomNodeProps>();

const emit = defineEmits<{
  close: [id: string];
  updateSize: [{ id: string; width: number; height: number }];
}>();

const width = ref<number>(400);
const height = ref<number>(400);
const components: Record<TComponent, Component> = {
  Component1: defineAsyncComponent(() => import("./Component1.vue")),
  Component2: defineAsyncComponent(() => import("./Component2.vue")),
};

const styled = computed(
  () =>
    `height: ${dimensions.height || 400}px;width: ${dimensions.width || 400}px`
);

function updateSize(val: OnResize) {
  if (val.params.width <= 200 || val.params.height <= 200) return;
  width.value = val.params.width;
  height.value = val.params.height;

  emit("updateSize", { id, width: width.value, height: height.value });
}
</script>

<template>
  <NodeResizer
    :min-width="200"
    :min-height="200"
    keep-aspect-ratio
    @resize="updateSize"
  />
  <div class="p-4 overflow-hidden" :style="styled">
    <component :is="components[componentName]" />
    <button
      @click="$emit('close', id)"
      class="absolute -top-3 -right-3 border border-black rounded-full text-xs bg-black text-white h-8 w-8 flex justify-center items-center hover:opacity-50"
    >
      X
    </button>
  </div>
</template>
