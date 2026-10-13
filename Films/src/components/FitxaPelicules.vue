<script setup>
import { ref } from 'vue'
import { mesInfo } from '@/services/communicationManager'

const props = defineProps({
    film: { type: Object, required: true }
})

const dialog = ref(false)
const info = ref({})

async function openInfo() {
    info.value = await mesInfo(props.film.imdbID)
    dialog.value = true
}
</script>

<template>
    <v-card class="my-card" rounded="lg">
        <img class="poster" :src="props.film.Poster" :alt="props.film.Title" />
        <p>{{ props.film.Title }}</p>
        <p>{{ props.film.Year }}</p>

        <v-dialog v-model="dialog" max-width="500">
            <template #activator="{ props: activatorProps }">
                <v-btn v-bind="activatorProps" @click="openInfo" color="surface-variant" text="Més informació"
                    variant="flat">
                </v-btn>
            </template>
            <v-card :title="props.film.Title">
                <v-card-text>
                    {{ info.Plot }}
                </v-card-text>

                <v-card-actions>
                    <v-spacer />
                    <v-btn @click="dialog = false">Tancar</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-card>
</template>

<style>
.my-card {
    text-align: center;
    padding-bottom: 10px;
    padding-top: 10px;
}

.poster {
    width: 250px;
    border-radius: 10px;
}

.search-bar {
    display: flex;
    align-items: center;
    gap: 12px;
    width: 500px;
}

.cercador {
    padding-top: 20px;
}

.button_cercar {
    width: 90px;
    height: 40px;
    background-color: rgb(200, 200, 200);
    color: black;
}
</style>