<script setup lang="ts">
import {ref} from 'vue';

const props = defineProps<{ descriptionTache: string, modelValue: boolean }>();
const emit = defineEmits<{
  supprimerTache: [],
  "update:modelValue": [boolean]
}
>();
</script>

<template>
  <input type="checkbox" @change="$emit('changerTacheFaite', ($event.target as HTMLInputElement).checked)"
         :checked="props.modelValue">
  <span :class="{fait: props.modelValue}">{{ props.descriptionTache }}</span>
  <button @click="emit('supprimerTache')">Retirer</button>
</template>

<style scoped>
.fait {
  text-decoration: line-through;
}
</style>
