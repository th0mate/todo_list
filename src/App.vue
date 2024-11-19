<script setup lang="ts">
import ListeDeTaches from '@/composants/ListeDeTaches.vue';
import {ref} from "vue";


const todoList = ref([

    {id: 0, titre: "Exemple"}
  ]
);

const nouvelleTache = ref('');

function ajouterListe() {
  if (nouvelleTache.value === '') {
    return;
  }

  todoList.value.push({
    id: todoList.value.length,
    titre: nouvelleTache.value
  });
  nouvelleTache.value = '';
}

interface Liste {
  id: number;
  titre: string;
}

function retirerListe(liste:Liste) {
  const index = todoList.value.indexOf(liste);
  todoList.value.splice(index, 1);
}

</script>

<template>
  <div class="wrapAdd">
    <input type="text" placeholder="Ajouter une liste" v-model.trim="nouvelleTache">
    <button @click="ajouterListe">Ajouter</button>
  </div>
  <br>

  <div v-for="todo in todoList" :key="todo.id">
    <ListeDeTaches :titre="todo.titre" @supprimerListe="retirerListe(todo)"/>
    <br>
  </div>
</template>

<style scoped>
</style>
