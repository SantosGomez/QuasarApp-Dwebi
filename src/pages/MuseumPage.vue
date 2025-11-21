<template>
  <q-page class="q-pa-md flex flex-center">
    <div class="q-gutter-md" style="max-width: 600px; width: 100%;">
      <q-btn color="primary" label="Obtener obra aleatoria" @click="fetchRandomArtwork" />

      <ArtworkCard
        v-if="artwork"
        :title="artwork.title"
        :artist="artwork.artist"
        :image="artwork.image"
        :date="artwork.date"
        :medium="artwork.medium"
        :classification="artwork.classification"
        :department="artwork.department"
        :description="artwork.description"
      />
    </div>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import ArtworkCard from 'components/ArtworkCard.vue'

const artwork = ref(null)

async function fetchRandomArtwork() {
  const randomId = Math.floor(Math.random() * 100000) 
  const response = await fetch(`https://api.artic.edu/api/v1/artworks/${randomId}`)
  const data = await response.json()

  if (data.data) {
    const art = data.data
    artwork.value = {
      title: art.title,
      artist: art.artist_title || 'Desconocido',
      image: art.image_id
        ? `https://www.artic.edu/iiif/2/${art.image_id}/full/843,/0/default.jpg`
        : null,
      date: art.date_display,
      medium: art.medium_display,
      classification: art.classification_title,
      department: art.department_title,
      description: art.thumbnail?.alt_text || 'Sin descripción disponible'
    }
  } else {
    artwork.value = null
  }
}

onMounted(fetchRandomArtwork)
</script>
