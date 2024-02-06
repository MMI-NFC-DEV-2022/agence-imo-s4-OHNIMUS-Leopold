<script setup lang="ts">
import { ref } from 'vue'
import AfficheMaison from './AfficheMaison.vue';

const maison = ref({});
</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">
                Résultat (Prévisualisation)
            </h2>
            <AfficheMaison v-bind="maison" />
        </div>
        <div class="p-2">
            <FormKit type="form" v-model="maison" 
            :config="{
            classes: {
            input: 'p-1 rounded border-gray-300 shadow-sm border',
            label: 'text-gray-600',
            },
            }"
            :submit-attrs="{ classes: { input: 'bg-red-300 p-1 rounded' } }">
                <FormKit name="nomMaison" label="nom" />
                <FormKit name="prix" label="prix" type="number" />
                <FormKit name="favori" label="Mettre en valeur" type="checkbox" wrapper-class="flex" />
            </FormKit>
        </div>
    </div>
</template>