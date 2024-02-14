<script setup lang="ts">
import { ref } from 'vue'
import AfficheQuartier from './AfficheQuartier.vue';
import { supabase } from '@/supabase';
import { useRouter } from 'vue-router'
import { useRoute } from 'vue-router'
const route = useRoute('/quartiers/edit/:id?')
const router = useRouter()

async function upsertQuartier(dataForm, node) {
    const { data, error } = await supabase.from("Quartier").upsert(dataForm).select();
    if (error) node.setErrors([error.message])
    else {
console.log({error,data});

        node.setErrors([]);
        router.push({ name: "quartiers-edit", params: { id: data[0].id } });
    }
}


const quartier = ref({});


if (route.params.id) {
    // On charge les données de la maison
    let { data, error } = await supabase
    .from("Quartier")
    .select("*")
    .eq("id", route.params.id);
    if (error) console.log("n'a pas pu charger le table Quartier :", error);
    else quartier.value = (data as any[])[0];
}


const { data: listeCommune, error } = await supabase
  .from("Commune")
  .select("*");
if (error) console.log("n'a pas pu charger la table Commune :", error);
// Les convertir par `map` en un tableau d'objets {value, label} pour FormKit
const optionsCommune = listeCommune?.map((commune) => ({
  value: commune.id,
  label: commune.nomCommune,
}));



</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">
                Résultat (Prévisualisation)
            </h2>
            <AfficheQuartier v-bind="quartier" />
        </div>
        <div class="p-2">
            <FormKit type="form" v-model="quartier" 
            @submit="upsertQuartier"
            :config="{
            classes: {
            input: 'p-1 rounded border-gray-300 shadow-sm border',
            label: 'text-gray-600',
            },
            }"
            :submit-attrs="{ classes: { input: 'bg-red-300 p-1 rounded' } }">
                <FormKit name="nomQuartier" label="nom" />
                <!-- <FormKit name="idCommune" label="Commune" /> -->
                <FormKit
                    type="select"
                    name="idCommune"
                    label="Commune"
                    :options="optionsCommune"
                />
                </FormKit>
            
        </div>
    </div>
</template>