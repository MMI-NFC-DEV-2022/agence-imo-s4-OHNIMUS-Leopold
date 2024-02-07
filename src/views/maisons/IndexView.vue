<script setup lang="ts">

import { SchemaOffreMaison } from '@/types';
import AfficheMaison from '@/components/AfficheMaison.vue';

import { supabase } from "@/supabase";
console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code
const maisons = []; // à remplacer par l'appel à Supabase

const res = await fetch('/data.json')
const tableauDeMaisons:SchemaOffreMaison[] = await res.json();



</script>

<template>
        <div class="flex">
                <AfficheMaison v-for="maison in tableauDeMaisons" v-bind="maison" :key="maison.id" />
        </div>
</template>