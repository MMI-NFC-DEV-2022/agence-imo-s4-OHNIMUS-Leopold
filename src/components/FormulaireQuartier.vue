< setup lang="ts">
import { ref } from 'vue'
import { supabase } from '@/supabase';
import { useRouter } from 'vue-router'
import { useRoute } from 'vue-router'
import { supabase } from '@/supabase';      
const route = useRoute('/quartiers/edit/:id?')
const router = useRouter()



const route = useRoute('/quartiers/edit/:id?')
const router = useRouter()

const quartier = ref({});

const communes = ref([]);

async function fetchCommunes() {
    const { data, error } = await supabase.from<Database>('Commune').select("*");
    if (error) console.log("Erreur lors du chargement des communes :", error);
    else communes.value = data;
}

fetchCommunes();

async function upsertQuartier(dataForm, node) {
    const { data, error } = await supabase.from<Database>('Quartier').upsert(dataForm).select();
    if (error) node.setErrors([error.message])
    else {
        console.log({error,data});
        node.setErrors([]);
        router.push({ name: "quartiers-edit", params: { id: data[0].id } });
    }
}

if (route.params.id) {
    let { data, error } = await supabase
    .from<Database>('Quartier')
    .select("*")
    .eq("id", route.params.id);
    if (error) console.log("n'a pas pu charger le table Quartier :", error);
    else quartier.value = (data as any[])[0];
}


</script>



<template>
    <div>
        <!-- Prévisualisation des données du quartier -->
        <div class="p-2">
            <h2 class="text-2xl">
                Résultat (Prévisualisation)
            </h2>
            {{ nomQuartier }}
            {{ nomCommune }}
            <!-- Assurez-vous d'avoir un composant pour afficher les détails du quartier -->
        </div>
        <!-- Formulaire du quartier -->
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
                <FormKit name="nomQuartier" label="Nom du quartier" />
                <!-- Champ de sélection pour la commune -->
                <FormKit name="idCommune" label="Commune" type="select">
                    <!-- Boucle à travers les communes pour peupler les options -->
                    <option v-for="commune in communes" :key="commune.id" :value="commune.id">{{ commune.nomCommune }}</option>
                </FormKit>
                <!-- Ajoutez d'autres champs nécessaires pour le quartier -->
            </FormKit>
        </div>
    </div>
</template>
