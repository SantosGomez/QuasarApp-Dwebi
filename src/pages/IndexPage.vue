<template>
  <div class="q-pa-md flex flex-center column">
    <q-btn outline style="color: goldenrod" label="Log-out" @click="logout" />
  </div>
  <div class="q-pa-xl column items-center justify-center">
    <h1 class="text-h4 q-mb-xl">Menú de APIs</h1>
    <q-btn label="PokeApi" color="primary" class="q-mb-lg" @click="goApi1" />
    <q-btn label="Museo Api" color="secondary" @click="goApi2" />
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
const router = useRouter()

function goApi1() {
  router.push('PokeApi')
}
function goApi2() {
  router.push('Museo')
}

function logout() {
  // Elimina el estado de login
  localStorage.removeItem('logged')

  // Redirige al login
  router.push('/login')
}
</script>
