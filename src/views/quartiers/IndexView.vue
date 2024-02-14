<script setup lang="ts">
import { supabase } from "../../supabase";
const { data, error } = await supabase.from('quartiercommune').select('*').order('nomCommune');
if (error) console.log("n'a pas pu charger la view quartiercommune :", error);

</script>

<template>
  <section class="flex flex-col">
    <h3 class="text-2xl">Liste des quartiers</h3>
    <!-- <ul>
      <li v-for="quartierObject in (data as any[])">
        {{ quartierObject.nomQuartier }} -
        {{ quartierObject.nomCommune }}
      </li>
    </ul> -->
    <ul>
      <li v-for="(listeQuartiers, nomCommune) in Object
      //@ts-ignore
      .groupBy( data, 
      //@ts-ignore
      v=>v.nomCommune  )">
        {{ nomCommune }}
        <p class="ml-5" v-for="quartierObject in listeQuartiers">
          <RouterLink :to="{ name:'quartiers-edit', params:{id:quartierObject.idQuartier} }">{{ quartierObject.nomQuartier }}</RouterLink>
        </p>
      </li>
    </ul>
  </section>
</template>