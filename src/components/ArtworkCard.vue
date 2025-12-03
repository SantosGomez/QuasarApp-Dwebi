<template>
  <div class="q-pa-md flex flex-center column text-center">
    <h2 class="text-h6 q-mb-xs">{{ title }}</h2>
    <p class="text-subtitle2 text-grey-5">{{ artist || 'Artista desconocido' }}</p>

    <q-img
      :src="image"
      :alt="title"
      class="q-mt-md shadow-2"
      style="max-width: 80%; border-radius: 12px;"
    />
    

    <div class="q-mt-md q-pa-sm bg-grey-9 text-white q-rounded-borders" style="max-width: 600px;">
      <p v-if="date" class="q-mb-xs"><strong>Fecha:</strong> {{ date }}</p>
      <p v-if="medium" class="q-mb-xs"><strong>Técnica:</strong> {{ medium }}</p>
      <p v-if="classification" class="q-mb-xs"><strong>Tipo:</strong> {{ classification }}</p>
      <p v-if="department" class="q-mb-xs"><strong>Departamento:</strong> {{ department }}</p>
      <p v-if="description" class="q-mt-sm text-grey-4">{{ description }}</p>
    </div>
  </div>

  
</template>

<script setup>
defineProps({
  title: String,
  artist: String,
  image: String,
  date: String,
  medium: String,
  classification: String,
  department: String,
  description: String
});
</script>
