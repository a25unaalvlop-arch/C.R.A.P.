<script setup>
import { ref } from 'vue'
import { cercar } from '@/services/communicationManager'
import FitxaPelicules from './FitxaPelicules.vue'

const cerca = ref('')
const resultats = ref([])

async function Buscar() {
  resultats.value = await cercar(cerca.value) || []
}

function clear() {
  cerca.value = ''
  resultats.value = []
}
</script>

<template>
  <div class="search-bar">
    <v-text-field v-model="cerca" label="Escriu la pel·lícula" variant="outlined" class="cercador" />
    <v-btn class="button_cercar" @click="Buscar">Cercar</v-btn>
    <v-btn class="button_cercar" @click="clear">Netejar</v-btn>
  </div>
  <v-row>
    <v-col v-for="film in resultats" :key="film.imdbID" cols="12" md="4">
      <FitxaPelicules :film="film" />
    </v-col>
  </v-row>
</template>

<style scoped></style>