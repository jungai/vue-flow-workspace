<script lang="ts" setup>
import type { TComponent } from "./types";
import { VueFlow, Node, useVueFlow } from "@vue-flow/core";
import CustomNode from "./components/CustomNode.vue";
import { ref, onMounted } from "vue";
import { v4 } from "uuid";

const LOCAL_STORAGE_KEY = "workspace";
const list: TComponent[] = ["Component1", "Component2"];
const elements = ref<Node[]>([]);
const eiei = ref<string>("🙂");

const { zoomIn, zoomOut, toObject } = useVueFlow();

function randomPosition() {
  return {
    x: Math.floor(Math.random() * (900 - 10 + 1)) + 10,
    y: Math.floor(Math.random() * (300 - 10 + 1)) + 10,
  };
}

function removeNode(id: string) {
  elements.value = elements.value.filter((v) => v.id != id);
}

function addNode(name: TComponent) {
  elements.value.push({
    id: v4(),
    type: "custom",
    data: {
      componentName: name,
    },
    position: randomPosition(),
  });
}

function handleSave() {
  localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(elements.value));
}

function clear() {
  elements.value = [];
  localStorage.removeItem(LOCAL_STORAGE_KEY);
}

onMounted(() => {
  const save = localStorage.getItem(LOCAL_STORAGE_KEY);
  if (save) {
    elements.value = JSON.parse(save);
  }
});

function test() {
  console.log("hello");
}
</script>

<template>
  <div class="m-auto h-screen w-full bg-slate-900 flex flex-col">
    <div class="h-200px p-4 flex justify-between items-center">
      <div class="text-4xl">{{ eiei }}</div>
      <div class="space-x-2">
        <button
          class="border border-pink-500 p-2 bg-white rounded-lg"
          @click="() => addNode('Component1')"
        >
          add Node1
        </button>
        <button
          class="border border-pink-500 p-2 bg-white rounded-lg"
          @click="() => addNode('Component2')"
        >
          add Node2
        </button>
        <button
          class="border border-pink-500 p-2 bg-white rounded-lg"
          @click="() => addNode(list[Math.floor(Math.random() * 2)])"
        >
          randomNode
        </button>
        <button
          class="border border-pink-500 p-2 bg-white rounded-lg"
          @click="clear"
        >
          clear
        </button>
        <button
          class="border border-pink-500 p-2 bg-white rounded-lg"
          @click="handleSave"
        >
          save
        </button>
      </div>
    </div>
    <VueFlow
      v-model="elements"
      class="flex-1"
      @node-drag="() => (eiei = '😀')"
      @node-drag-stop="() => (eiei = '🙂')"
    >
      <template #node-custom="{ data, id }">
        <CustomNode
          :component-name="data.componentName"
          :id="id"
          @close="removeNode"
        />
      </template>
      <div
        class="absolute z-[10] bottom-0 right-0 flex flex-col border border-pink-500 rounded-lg bg-white m-4 cursor-pointer"
      >
        <button class="p-2" @click="() => zoomIn()">+</button>
        <span class="text-xs p-2"
          >{{ Math.floor(toObject().zoom * 100) }}%</span
        >
        <button class="p-2" @click="() => zoomOut()">-</button>
      </div>
    </VueFlow>
  </div>
</template>

<style>
@import "@vue-flow/core/dist/style.css";
@import "@vue-flow/core/dist/theme-default.css";
</style>
