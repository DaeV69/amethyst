<script setup lang="ts">
import { useVModel } from "@vueuse/core";
const props = defineProps<{ modelValue?: number | string }>();
const emits = defineEmits(["update:modelValue"]);
const value = useVModel(props, "modelValue", emits);
</script>
  
<template>
  <input type="range" v-model="value">
</template>

<style scoped>
input[type=range] {
  transition: 200ms ease;
}

input[type=range] {
  background: rgb(var(--surface-600));
  border-radius: 4px;
  height: 6px;
  overflow: hidden;
  -webkit-appearance: none;
}

input[type='range']::-webkit-slider-thumb {
  width: 0px;
  box-shadow: -8000px 0 0 8000px rgb(var(--primary-900));
  -webkit-appearance: none;
}
</style>

