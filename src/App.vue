<script setup lang="ts">
import {ref} from 'vue';

const nouvelleTache = ref('');
let id = 0;
const taches = ref([
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

function retirerTache(tache) {
  const index = taches.value.indexOf(tache);
  taches.value.splice(index, 1);
}

</script>

<template>
  <input type="text" placeholder="Ajouter une tâche" v-model.trim="nouvelleTache">
  <button @click="ajouterTache">Ajouter</button>
  <div id="wrapper">
    <ul>
      <li v-for="tache in taches" :key="tache.id">
        <label :for="tache.id" :class="{fait : tache.faite}"><input type="checkbox" :id=tache.id v-model="tache.faite">{{ tache.description }}</label>
        <button @click="retirerTache(tache)">Retirer</button>
      </li>
    </ul>
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
