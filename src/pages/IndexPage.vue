<script setup>
import { ref } from 'vue'
import pokeApi from 'src/services/pokeApi'

const pokemon = ref(null)
const loading = ref(false)
const error = ref(null)
const search = ref('charmander') // Valor inicial

const fetchPokemon = async () => {
  if (!search.value) return

  loading.value = true
  error.value = null
  pokemon.value = null

  try {
    const { data } = await pokeApi.get(`/pokemon/${search.value.toLowerCase()}`)
    pokemon.value = data
  } catch (e) {
    console.error(e)
    error.value = 'Ese Pokémon no existe (o se nos escapó :c)'
  } finally {
    loading.value = false
  }
}

// Cargar el primero al inicio
fetchPokemon()

import { useRouter } from 'vue-router'

const router = useRouter()

function logout() {
  // Elimina el estado de login
  localStorage.removeItem('logged')

  // Redirige al login
  router.push('/login')
}
</script>

<template>
  <div class="q-pa-md flex flex-center column">
    <q-btn outline style="color: goldenrod" label="Log-out" @click="logout" />
  </div>
  <div class="q-pa-md flex flex-center column">
    <!-- Input para buscar Pokémon -->
    <div class="q-pa-md" style="width: 300px">
      <q-input
        v-model="search"
        label="Nombre del Pokémon"
        filled
        @keyup.enter="fetchPokemon"
        :disable="loading"
      >
        <template #append>
          <q-btn icon="las la-search" round flat @click="fetchPokemon" :loading="loading" />
        </template>
      </q-input>
    </div>

    <!-- Estados -->
    <div v-if="loading" class="q-mt-md">Buscando Pokémon…</div>
    <div v-else-if="error" class="q-mt-md text-red">{{ error }}</div>

    <!-- Card con la info -->
    <q-card v-else-if="pokemon" class="my-card q-mt-md" bordered>
      <q-img :src="pokemon.sprites.front_default" style="width: 200px; margin: auto" />

      <q-card-section>
        <div class="text-h6 text-bold text-center text-yellow-10">
          {{ pokemon.name.toUpperCase() }}
        </div>
      </q-card-section>

      <q-separator />

      <q-card-section>
        <div class="text-subtitle2 text-bold">Stats:</div>
        <ul>
          <li v-for="stat in pokemon.stats" :key="stat.stat.name">
            {{ stat.stat.name.toUpperCase() }}: {{ stat.base_stat }}
          </li>
        </ul>
      </q-card-section>
    </q-card>
  </div>
</template>

<style>
.my-card {
  width: 280px;
  border-radius: 12px;
  background-color: #fffbea;
}
</style>
