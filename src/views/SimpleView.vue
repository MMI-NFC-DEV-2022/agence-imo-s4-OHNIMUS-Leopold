<script setup lang="ts">

import { type SchemaOffreMaison } from '@/types';
import AfficheMaison from '../components/AfficheMaison.vue';

const maMaison:SchemaOffreMaison = {
    nomMaison: 'Maison2',
    prix: 1000,
    adresse: '123 rue',
    nbrChambres: 3,
    nbrSDB: 2,
    surface: "30x40m²",
    favori: true,
    image: 'pexels-binyamin-mellish-106399 1 (5).png'
}
</script>

<template>

    
    on passe les valeurs en objet avec v-bind
<AfficheMaison v-bind:nom-maison="maMaison.nomMaison" :prix="maMaison.prix" :favori="maMaison.favori" />
        on passe les valeurs en attributs
        <AfficheMaison nom-maison="Maison" :favori="true" image="pexels-binyamin-mellish-106399.png" />
</template>