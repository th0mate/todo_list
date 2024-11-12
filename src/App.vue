<script setup lang="ts">
import {ref} from 'vue';

const texte = "un texte qui s'affiche";
const urlVue = "https://vuejs.org/";

const compteur = ref(7);

function incremente() {
  compteur.value++;
}
</script>


<template>
  <div id="wrapper">
    <h1>TODO liste</h1>
    <p>{{ texte }}</p>
    <a v-bind:href="urlVue">Le site de vue</a>
    <button v-on:click="incremente">+</button>
    <p>{{ compteur }}</p>
    <input v-model="compteur">
  </div>
</template>

<style scoped>
</style>
