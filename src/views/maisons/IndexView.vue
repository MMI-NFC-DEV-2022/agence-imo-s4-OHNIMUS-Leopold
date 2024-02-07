<script setup lang="ts">

import AfficheMaison from '@/components/AfficheMaison.vue';
import { supabase } from "@/supabase";
console.log("supabase :", supabase); 

const { data: lesMaisons, error } = await supabase.from('Maison').select('*')

</script>



<template>
        <div class="flex">
            <AfficheMaison v-for="maison in lesMaisons" v-bind="maison" />
        </div>
</template>