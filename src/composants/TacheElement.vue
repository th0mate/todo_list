<script setup lang="ts">

const props = defineProps<{ modelValue: boolean }>();
const emit = defineEmits<{
  supprimerTache: [],
  "update:modelValue": [boolean]
}
>();
</script>

<template>
  <input type="checkbox" @change="$emit('update:modelValue', ($event.target as HTMLInputElement).checked)"
         :checked="props.modelValue">
  <span :class="{fait: props.modelValue}"><slot></slot></span>
  <button @click="emit('supprimerTache')">Retirer</button>
</template>

<style scoped>
.fait {
  text-decoration: line-through;
}
</style>
