<script setup lang="ts">
import {ref, computed} from 'vue';
import type {Ref} from 'vue';
import TacheElement from '@/composants/TacheElement.vue';

const emit = defineEmits<{ supprimerListe: [] }>();

const props = defineProps<{ titre: string }>();

const nouvelleTache = ref('');
const cacheFaits = ref(false);
let id = 0;
const tachesFiltrees = computed(filtrerTaches);

const taches: Ref<Tache[]> = ref([
  {id: id++, description: "Apprendre Vue", faite: true},
  {id: id++, description: "Finir la SAÉ", faite: false},
  {id: id++, description: "Réviser pour l'interro", faite: false}
]);

function ajouterTache() {

  if (nouvelleTache.value === '') {
    return;
  }

  taches.value.push({
    id: id++,
    description: nouvelleTache.value,
    faite: false
  });
  nouvelleTache.value = '';
}

interface Tache {
  id: number;
  description: string;
  faite: boolean;
}

function retirerTache(tache: Tache) {
  const index = taches.value.indexOf(tache);
  taches.value.splice(index, 1);
}

function filtrerTaches() {
  return cacheFaits.value ? taches.value.filter(tache => !tache.faite) : taches.value;
}

</script>

<template>

  <div id="wrapper">
    <button @click="emit('supprimerListe')">x</button>
    <h2>{{ props.titre }}</h2>
    <input type="text" placeholder="Ajouter une tâche" v-model.trim="nouvelleTache">
    <button @click="ajouterTache">Ajouter</button>
    <ul>
      <li v-for="tache in tachesFiltrees" :key="tache.id">
        <TacheElement
          :description-tache="tache.description"
          v-model="tache.faite"
          @supprimer-tache="retirerTache(tache)"
        />
      </li>
    </ul>

    <button @click="cacheFaits = !cacheFaits">
      {{ cacheFaits ? 'Tout montrer' : 'Cacher les tâches terminées' }}
    </button>
  </div>
</template>

<style scoped>
#wrapper {
  border-radius: 5px;
  border: solid black 2px;
  padding: 10px;
}

ul, label {
  padding: 10px;
}

li {
  list-style: none;
  padding: 2px 0px;
}

.fait {
  text-decoration: line-through;
}
</style>
