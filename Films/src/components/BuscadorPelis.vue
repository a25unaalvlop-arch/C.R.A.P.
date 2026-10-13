<script setup>

import { ref } from 'vue'
import { cercar } from '@/services/communicationManager'
import { mesInfo } from '@/services/communicationManager'
import FitxaPelicules from './FitxaPelicules.vue'

const cerca = ref('')
const resultats = ref([])
const info = ref({})

async function Buscar() {
  resultats.value = await cercar(cerca.value)
  info.value = {}
}

async function clear() {
  resultats.value = []
  info.value = {}
  cerca.value = ''
}

async function Info(imdbID) {
  info.value[imdbID] = await mesInfo(imdbID)
}

</script>

<template>
  <div class="search-bar">
    <v-text-field class="cercador" variant="outlined" v-model="cerca" label="Escriu la pel·licula"></v-text-field>
    <v-btn class="button_cercar" @click="Buscar">Cercar</v-btn>
    <v-btn class="button_cercar" @click="clear">Netejar</v-btn>
  </div>
  <v-row>

    <v-col v-for="film in resultats" :key="film.imdbID" cols="12" md="4">
      <FitxaPelicules
        :film="film"
        :info="info[film.imdbID]"
        @request-info="Info"
      />

    </v-col>

  </v-row>

</template>

<style scoped>

</style>