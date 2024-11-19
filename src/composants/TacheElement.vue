<script setup lang="ts">
import {ref} from 'vue';

const props = defineProps<{ descriptionTache: string, cochee: boolean }>();
const emit = defineEmits<{
  supprimerTache: [],
  changerTacheFaite: [boolean]
}
>();
</script>

<template>
  <input type="checkbox" @change="$emit('changerTacheFaite', ($event.target as HTMLInputElement).checked)"
         :checked="props.cochee">
  <span :class="{fait: props.cochee}">{{ props.descriptionTache }}</span>
  <button @click="emit('supprimerTache')">Retirer</button>
</template>

<style scoped>
.fait {
  text-decoration: line-through;
}
</style>
