<template>
  <q-page class="flex flex-center">
    <q-parallax src="https://concepto.de/wp-content/uploads/2019/05/servidor-e1557165670831.jpg ">
      <q-card class="q-pa-lg" flat bordered style="width: 350px">
        <q-card-section class="text-h6 text-center"> Iniciar Sesión </q-card-section>

        <q-card-section>
          <q-input v-model="email" label="Email" filled />
          <q-input v-model="password" type="password" label="Contraseña" filled class="q-mt-md" />
        </q-card-section>

        <q-card-actions align="center">
          <q-btn color="primary" label="Entrar" @click="login" />
        </q-card-actions>

        <q-card-section v-if="error" class="text-negative text-center">
          {{ error }}
        </q-card-section>
      </q-card>
    </q-parallax>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const error = ref('')
const router = useRouter()

const login = () => {
  if (email.value === 'admin@uttn.mx' && password.value === '12345678') {
    router.push('/') // tu página principal
  } else {
    error.value = 'Credenciales incorrectas'
  }
}
</script>
