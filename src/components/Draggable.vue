<template>
  <rect v-bind="props" :fill="color" @mousedown="onmousedown" />
</template>

<script setup>
const props = defineProps({
  id: { type: String, required: true },
  x: { type: Number, required: true },
  y: { type: Number, required: true },
  width: { type: Number, default: 100 },
  height: { type: Number, default: 100 },
  color: { type: String, default: 'red' },
});

const emit = defineEmits(['dragStarted']);

function onmousedown($event) {
  emit('dragStarted', {
    id: props.id,
    x: $event.clientX - props.x,
    y: $event.clientY - props.y
  })
}
</script>