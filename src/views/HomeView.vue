<template>
  <svg v-if="blocks" @mousemove="onmousemove" @mouseup="cancel" @mouseleave.prevent.stop="cancel">
    <Draggable v-for="block in blocks" v-bind="block" @drag-started="startDrag" />
  </svg>
</template>


<script setup>
import Draggable from "../components/Draggable.vue";
import { ref } from 'vue'
import data from "../assets/blocks.json"

const blocks = ref(data);
const dragged = ref('');
const offset = ref({ x: 0, y: 0 });

const startDrag = function({ id, x, y }) {
  offset.value.x = x;
  offset.value.y = y;
  dragged.value = id;
}

function onmousemove($event) {
  const block = findDraggable(dragged.value);
  block.x = $event.clientX - offset.value.x;
  block.y = $event.clientY - offset.value.y;
}

function findDraggable(id) {
  const found = blocks.value.find(i => i.id === id);
  return found ?? { x: 0, y: 0 };
}

function cancel() {
  dragged.value = ''
}
</script>

<style scoped>
svg {
  height: 100vh;
  width: 100vw;
}
</style>