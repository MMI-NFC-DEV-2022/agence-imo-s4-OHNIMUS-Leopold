<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div>
      <nav class="space-x-2">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/simple">Simple</RouterLink>
        <RouterLink to="/formkit">Formkit</RouterLink>
        <RouterLink to="/maisons">IndexMaisons</RouterLink>
        <RouterLink to="/auth">Auth</RouterLink>
      </nav>
    </div>
  </header>

  <Suspense>
    <RouterView />
  </Suspense>
</template>
