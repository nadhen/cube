<template>
  <div>
    <div v-if="error.statusCode == 500">
      <h2>{{ error.statusCode }}</h2>
      <button @click="handleError">Clear errors</button>
    </div>
    <div else>
      <404Page />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: Object as () => NuxtError
})

const handleError = () => clearError({ redirect: '/' })
</script>